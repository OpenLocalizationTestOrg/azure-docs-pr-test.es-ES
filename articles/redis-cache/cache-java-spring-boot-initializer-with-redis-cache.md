---
title: "aaaHow tooconfigure una toouse de aplicación Spring arranque inicializador caché en Redis"
description: "Obtenga información acerca de cómo tooconfigure una aplicación de arranque del muelle creado con hello primavera Initializr toouse caché en Redis de Azure."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Redis Cache
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="5dfaa-104">¿Cómo tooconfigure una toouse de aplicación Spring arranque inicializador caché en Redis</span><span class="sxs-lookup"><span data-stu-id="5dfaa-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="5dfaa-105">Información general</span><span class="sxs-lookup"><span data-stu-id="5dfaa-105">Overview</span></span>

<span data-ttu-id="5dfaa-106">Hola  **[Spring Framework]**  es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="5dfaa-107">Uno de los proyectos de más populares de Hola que se basa en dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones independientes de Java.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="5dfaa-108">los desarrolladores de toohelp comenzar con el arranque de primavera, varios paquetes de arranque de primavera de ejemplo están disponibles en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="5dfaa-109">Además toochoosing de lista de Hola de arranque básica de primavera de proyectos, hello  **[primavera Initializr]**  ayuda a los desarrolladores a empezar a trabajar con la creación de aplicaciones de arranque Spring personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="5dfaa-110">Este artículo le guiará por la creación de una caché en Redis mediante el portal de Azure, a continuación, usar Hola Hola **Initializr primavera** toocreate web de una aplicación personalizada y, a continuación, crear un Java aplicación que almacena y recupera datos mediante el Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dfaa-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5dfaa-111">Prerequisites</span></span>

<span data-ttu-id="5dfaa-112">Hola siguiendo los requisitos previos es necesarios en los pasos de orden toofollow hello en este artículo:</span><span class="sxs-lookup"><span data-stu-id="5dfaa-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="5dfaa-113">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="5dfaa-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="5dfaa-114">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="5dfaa-115">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="5dfaa-116">Crear una caché de Redis en Azure</span><span class="sxs-lookup"><span data-stu-id="5dfaa-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="5dfaa-117">Examinar toohello Azure portal en <https://portal.azure.com/> y haga clic en elemento de Hola para **+ nuevo**.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="5dfaa-119">Haga clic en **Base de datos** y luego en **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="5dfaa-121">En hello **nueva caché en Redis** escriba hello **nombre DNS** para la memoria caché, a continuación, especifique la **suscripción**, **grupo de recursos**,  **Ubicación**, y **tarifa**.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="5dfaa-122">Cuando se han especificado estas opciones, haga clic en **crear** toocreate la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="5dfaa-124">Una vez que se ha completado la memoria caché, verá aparece en su Azure **panel**, así como en hello **todos los recursos**, y **memorias caché Redis** páginas.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="5dfaa-125">Puede hacer clic en la memoria caché en cualquiera de esos página de propiedades de ubicaciones tooopen hello de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="5dfaa-127">Cuando se muestra la página de Hola que contiene la lista de Hola de propiedades de la memoria caché, haga clic en **las claves de acceso** y copie las claves de acceso de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="5dfaa-129">Crear una aplicación personalizada con hello Initializr primavera</span><span class="sxs-lookup"><span data-stu-id="5dfaa-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="5dfaa-130">Examinar demasiado<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="5dfaa-131">Especifique que desea toogenerate una **Maven** proyecto con **Java**, escriba Hola **grupo** y **Aritifact** nombres para la aplicación, y, a continuación, haga clic en el vínculo de hello demasiado**versión completa de conmutador toohello** de hello primavera Initializr.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="5dfaa-133">Hola primavera Initializr usará hello **grupo** y **Aritifact** nombre del paquete de nombres toocreate Hola; por ejemplo: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="5dfaa-134">Desplácese hacia abajo toohello **Web** y la sección de casilla hello para **Web**, a continuación, desplácese hacia abajo toohello **NoSQL** y la sección de casilla hello para **Redis**, a continuación, desplácese toohello inferior de la página de Hola y haga clic en botón Hola demasiado**generar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Opciones completas de Spring Initializr][SI02]

1. <span data-ttu-id="5dfaa-136">Cuando se le solicite, descargue la ruta de acceso de hello proyecto tooa en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot][SI03]

1. <span data-ttu-id="5dfaa-138">Una vez extraídos los archivos de hello en el sistema local, la aplicación de arranque de primavera personalizada estará lista para su edición.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto personalizados de Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="5dfaa-140">Configure su toouse Spring arranque personalizado en la caché de Redis</span><span class="sxs-lookup"><span data-stu-id="5dfaa-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="5dfaa-141">Busque hello *application.properties* archivo Hola *recursos* directorio de la aplicación, o crear el archivo hello si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Busque el archivo de hello application.properties][RE01]

1. <span data-ttu-id="5dfaa-143">Abra hello *application.properties* un archivo en un editor de texto y agregue Hola líneas toohello archivo siguiente y reemplace los valores de ejemplo de Hola con propiedades adecuadas de Hola desde la memoria caché:</span><span class="sxs-lookup"><span data-stu-id="5dfaa-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Editar archivo de hello application.properties][RE02]

1. <span data-ttu-id="5dfaa-145">Guarde y cierre hello *application.properties* archivo.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="5dfaa-146">Cree una carpeta denominada *controlador* bajo la carpeta de origen de hello para el paquete; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5dfaa-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="5dfaa-147">O bien</span><span class="sxs-lookup"><span data-stu-id="5dfaa-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="5dfaa-148">Crear un nuevo archivo denominado *HelloController.java* en hello *controlador* carpeta.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="5dfaa-149">Abra el archivo hello en un editor de texto y agregue Hola después tooit de código:</span><span class="sxs-lookup"><span data-stu-id="5dfaa-149">Open hello file in a text editor and add hello following code tooit:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="5dfaa-150">Necesitará tooreplace `com.contoso.myazuredemo` con el nombre de paquete de hello para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="5dfaa-151">Guarde y cierre hello *HelloController.java* archivo.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="5dfaa-152">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5dfaa-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="5dfaa-153">Probar la aplicación web de hello examinando toohttp://localhost:8080 mediante un explorador web o utilizar una sintaxis de hello como Hola siguiente ejemplo, si tienes curl disponible:</span><span class="sxs-lookup"><span data-stu-id="5dfaa-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="5dfaa-154">Debería ver Hola "¡Hello World!"</span><span class="sxs-lookup"><span data-stu-id="5dfaa-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="5dfaa-155">del controlador de ejemplo mostrado, que se está recuperando dinámicamente de la memoria caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="5dfaa-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dfaa-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5dfaa-156">Next steps</span></span>

<span data-ttu-id="5dfaa-157">Para obtener más información sobre el uso de las aplicaciones de arranque del muelle en Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="5dfaa-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="5dfaa-158">Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello</span><span class="sxs-lookup"><span data-stu-id="5dfaa-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="5dfaa-159">Ejecuta una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="5dfaa-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="5dfaa-160">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="5dfaa-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="5dfaa-161">Para obtener más información sobre cómo obtener iniciado con caché en Redis de Java en Azure, consulte [cómo toouse caché de Redis de Azure con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="5dfaa-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[arranque primavera]: http://projects.spring.io/spring-boot/
[primavera Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
