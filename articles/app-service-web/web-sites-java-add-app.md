---
title: "Incorporación de una aplicación de Java a Aplicaciones web del Servicio de aplicaciones de Azure"
description: "Este tutorial muestra cómo agregar una página o aplicación a su instancia de Aplicaciones web del Servicio de aplicaciones de Azure que ya está configurado para usar Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="338da-103">Incorporación de una aplicación de Java a Aplicaciones web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="338da-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="338da-104">Cuando haya inicializado la aplicación web de Java en [Azure App Service][Azure App Service] tal como se documenta en [Creación de una aplicación web de Java en Azure App Service](web-sites-java-get-started.md), podrá cargar su aplicación colocando su WAR en la carpeta **webapps**.</span><span class="sxs-lookup"><span data-stu-id="338da-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="338da-105">La ruta de acceso de navegación a la carpeta **webapps** varía en función de cómo haya configurado la instancia de Aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="338da-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="338da-106">Si configura su aplicación web con Azure Marketplace, la ruta de acceso a la carpeta **webapps** tiene el formato **d:\home\site\wwwroot\bin\application\_server\webapps**, donde **application\_server** es el nombre del servidor de la aplicación vigente en su instancia de Web Apps.</span><span class="sxs-lookup"><span data-stu-id="338da-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="338da-107">Si configura su aplicación web con la interfaz de usuario de configuración de Azure, la ruta de acceso a la carpeta **webapps** tiene el formato **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="338da-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="338da-108">Tenga en cuenta que puede utilizar el control de código fuente para cargar la aplicación o páginas web, incluso en [escenarios de integración continua](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="338da-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="338da-109">FTP también es una opción para cargar la aplicación o las páginas web; para más información sobre cómo implementar las aplicaciones a través de FTP, consulte [Documentación de implementación de Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="338da-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="338da-110">Nota para aplicaciones web de Tomcat: después de cargar el archivo WAR a la carpeta **webapps** , el servidor de la aplicación Tomcat detectará que lo ha agregado y lo cargará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="338da-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="338da-111">Tenga en cuenta que si copia los archivos (excepto los archivos WAR) al directorio raíz, será necesario reiniciar el servidor de aplicaciones antes de utilizar esos archivos.</span><span class="sxs-lookup"><span data-stu-id="338da-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="338da-112">La funcionalidad de carga automática para las aplicaciones web de Java de Tomcat que se ejecutan en Azure se basa en un nuevo archivo WAR que se agrega, o en archivos o directorios nuevos que se agregan a la carpeta **webapps** .</span><span class="sxs-lookup"><span data-stu-id="338da-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="338da-113">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="338da-113">See Also</span></span>
<span data-ttu-id="338da-114">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure].</span><span class="sxs-lookup"><span data-stu-id="338da-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="338da-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="338da-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="338da-116">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="338da-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="338da-117">[Documentación de implementación de Azure App Service]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="338da-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
