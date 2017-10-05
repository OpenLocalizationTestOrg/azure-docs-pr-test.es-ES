---
title: "Conexión a una carpeta del sistema de archivos local desde Azure Logic Apps | Microsoft Docs"
description: "Conexión a sistemas de archivos locales desde el flujo de trabajo de la aplicación lógica a través de la puerta de enlace de datos local y el conector del sistema de archivos"
keywords: Sistemas de archivos
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="b2695-104">Conexión a sistemas de archivos locales desde las aplicaciones lógicas con el conector de sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="b2695-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="b2695-105">La conectividad de nube híbrida es fundamental para las aplicaciones lógicas y para administrar datos y acceder de forma segura a recursos locales, las aplicaciones lógicas pueden utilizar la puerta de enlace de datos local.</span><span class="sxs-lookup"><span data-stu-id="b2695-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="b2695-106">En este artículo, mostramos cómo conectarse a un sistema de archivos local con un escenario básico: copiar un archivo que se carga en Dropbox para un recurso compartido de archivos y, después, enviar un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b2695-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2695-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b2695-107">Prerequisites</span></span>

- <span data-ttu-id="b2695-108">Instale y configure la [puerta de enlace de datos local](https://www.microsoft.com/download/details.aspx?id=53127) más reciente.</span><span class="sxs-lookup"><span data-stu-id="b2695-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="b2695-109">Instale la puerta de enlace de datos local más reciente, versión 1.15.6150.1 o superior.</span><span class="sxs-lookup"><span data-stu-id="b2695-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="b2695-110">En [Conexión a la puerta de enlace de datos local](http://aka.ms/logicapps-gateway) se enumeran los pasos.</span><span class="sxs-lookup"><span data-stu-id="b2695-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="b2695-111">La puerta de enlace debe instalarse en una máquina local para poder continuar con el resto de los pasos.</span><span class="sxs-lookup"><span data-stu-id="b2695-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="b2695-112">Incorporación de desencadenadores y acciones para conectarse al sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="b2695-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="b2695-113">Cree una aplicación de la lógica y agregue el desencadenador **Dropbox - Cuando se crea un archivo**.</span><span class="sxs-lookup"><span data-stu-id="b2695-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="b2695-114">En el desencadenador, elija **Paso siguiente** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="b2695-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="b2695-115">En el cuadro de búsqueda, escriba `file system` para poder ver todas las acciones admitidas para el conector del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="b2695-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![Conector Buscar archivo](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="b2695-117">Elija la acción **Crear archivo** y cree una conexión con el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="b2695-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="b2695-118">Si no tiene una conexión existente, se le pedirá que cree una.</span><span class="sxs-lookup"><span data-stu-id="b2695-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="b2695-119">Seleccione **Connect via on-premises data gateway** (Conectarse a través de la puerta de enlace de datos local).</span><span class="sxs-lookup"><span data-stu-id="b2695-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="b2695-120">Aparecen más propiedades.</span><span class="sxs-lookup"><span data-stu-id="b2695-120">More properties appear.</span></span>
   2. <span data-ttu-id="b2695-121">Seleccione la carpeta raíz para el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="b2695-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="b2695-122">La carpeta raíz es la carpeta primaria principal, que se usa para las rutas de acceso relativas para todas las acciones relacionadas con archivos.</span><span class="sxs-lookup"><span data-stu-id="b2695-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="b2695-123">Puede especificar una carpeta local en la máquina en la que está instalada la puerta de enlace de datos local; o bien, la carpeta puede ser un recurso compartido de red al que tiene acceso la máquina.</span><span class="sxs-lookup"><span data-stu-id="b2695-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="b2695-124">Escriba el nombre de usuario y la contraseña para la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b2695-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="b2695-125">Seleccione la puerta de enlace que ha instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b2695-125">Select the gateway that you previously installed.</span></span>

       ![Configuración de la conexión](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="b2695-127">Después de proporcionar todos los detalles, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b2695-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="b2695-128">Logic Apps configura y comprueba la conexión, asegurándose de que la conexión funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="b2695-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="b2695-129">Si la conexión se configura correctamente, verá opciones para la acción que ha seleccionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b2695-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="b2695-130">El conector de sistema de archivos ahora está listo para usarse.</span><span class="sxs-lookup"><span data-stu-id="b2695-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="b2695-131">Especifique que desea copiar archivos desde Dropbox a la carpeta raíz para el recurso compartido de archivos local.</span><span class="sxs-lookup"><span data-stu-id="b2695-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![Acción Crear archivo](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="b2695-133">Después de la aplicación lógica copie el archivo, agregue una acción de Outlook que envíe un correo electrónico para que los usuarios correspondientes lo sepan.</span><span class="sxs-lookup"><span data-stu-id="b2695-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="b2695-134">Especifique los destinatarios, el título y el cuerpo del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b2695-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="b2695-135">En el selector de contenido dinámico, puede elegir salidas de datos desde el conector de archivos para que pueda agregar más detalles al correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b2695-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![Acción Enviar correo electrónico](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="b2695-137">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="b2695-137">Save your logic app.</span></span> <span data-ttu-id="b2695-138">Pruebe la aplicación cargando archivos en Dropbox.</span><span class="sxs-lookup"><span data-stu-id="b2695-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="b2695-139">El archivo se debe copiar en el recurso compartido local de archivos y debe recibir un correo electrónico acerca de la operación.</span><span class="sxs-lookup"><span data-stu-id="b2695-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="b2695-140">Aprenda cómo [supervisar las aplicaciones lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b2695-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="b2695-141">Enhorabuena, ahora tiene una aplicación lógica que funciona y que se puede conectar a su sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="b2695-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="b2695-142">Intente explorar otras funcionalidades ofrecidas por el conector, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b2695-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="b2695-143">Crear archivo</span><span class="sxs-lookup"><span data-stu-id="b2695-143">Create file</span></span>
- <span data-ttu-id="b2695-144">Enumerar archivos de la carpeta</span><span class="sxs-lookup"><span data-stu-id="b2695-144">List files in folder</span></span>
- <span data-ttu-id="b2695-145">Anexar archivo</span><span class="sxs-lookup"><span data-stu-id="b2695-145">Append file</span></span>
- <span data-ttu-id="b2695-146">Eliminar archivo</span><span class="sxs-lookup"><span data-stu-id="b2695-146">Delete file</span></span>
- <span data-ttu-id="b2695-147">Obtener contenido de archivo</span><span class="sxs-lookup"><span data-stu-id="b2695-147">Get file content</span></span>
- <span data-ttu-id="b2695-148">Obtener contenido de archivo mediante la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="b2695-148">Get file content using path</span></span>
- <span data-ttu-id="b2695-149">Obtener metadatos de archivo</span><span class="sxs-lookup"><span data-stu-id="b2695-149">Get file metadata</span></span>
- <span data-ttu-id="b2695-150">Obtener metadatos de archivo mediante la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="b2695-150">Get file metadata using path</span></span>
- <span data-ttu-id="b2695-151">Enumerar archivos de la carpeta raíz</span><span class="sxs-lookup"><span data-stu-id="b2695-151">List files in root folder</span></span>
- <span data-ttu-id="b2695-152">Actualizar archivo</span><span class="sxs-lookup"><span data-stu-id="b2695-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="b2695-153">Visualización de Swagger</span><span class="sxs-lookup"><span data-stu-id="b2695-153">View the swagger</span></span>
<span data-ttu-id="b2695-154">Vea los [detalles de Swagger](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="b2695-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="b2695-155">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="b2695-155">Get help</span></span>

<span data-ttu-id="b2695-156">Para formular preguntas, o responderlas, y saber lo que hacen otros usuarios de Azure Logic Apps, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="b2695-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="b2695-157">Para ayudar a mejorar Azure Logic Apps y los conectores, vote o envíe ideas en el [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="b2695-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2695-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2695-158">Next steps</span></span>

- <span data-ttu-id="b2695-159">[Conexión a datos locales](../logic-apps/logic-apps-gateway-connection.md) desde aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="b2695-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="b2695-160">Aprenda sobre la [integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2695-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
