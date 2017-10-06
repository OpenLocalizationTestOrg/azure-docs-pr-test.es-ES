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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>¿Cómo tooconfigure una toouse de aplicación Spring arranque inicializador caché en Redis

## <a name="overview"></a>Información general

Hola  **[Spring Framework]**  es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos de más populares de Hola que se basa en dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones independientes de Java. los desarrolladores de toohelp comenzar con el arranque de primavera, varios paquetes de arranque de primavera de ejemplo están disponibles en <https://github.com/spring-guides/>. Además toochoosing de lista de Hola de arranque básica de primavera de proyectos, hello  **[primavera Initializr]**  ayuda a los desarrolladores a empezar a trabajar con la creación de aplicaciones de arranque Spring personalizadas.

Este artículo le guiará por la creación de una caché en Redis mediante el portal de Azure, a continuación, usar Hola Hola **Initializr primavera** toocreate web de una aplicación personalizada y, a continuación, crear un Java aplicación que almacena y recupera datos mediante el Caché en Redis.

## <a name="prerequisites"></a>Requisitos previos

Hola siguiendo los requisitos previos es necesarios en los pasos de orden toofollow hello en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].

* Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.

* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-a-redis-cache-on-azure"></a>Crear una caché de Redis en Azure

1. Examinar toohello Azure portal en <https://portal.azure.com/> y haga clic en elemento de Hola para **+ nuevo**.

   ![Azure Portal][AZ01]

1. Haga clic en **Base de datos** y luego en **Redis Cache**.

   ![Azure Portal][AZ02]

1. En hello **nueva caché en Redis** escriba hello **nombre DNS** para la memoria caché, a continuación, especifique la **suscripción**, **grupo de recursos**,  **Ubicación**, y **tarifa**. Cuando se han especificado estas opciones, haga clic en **crear** toocreate la memoria caché.

   ![Azure Portal][AZ03]

1. Una vez que se ha completado la memoria caché, verá aparece en su Azure **panel**, así como en hello **todos los recursos**, y **memorias caché Redis** páginas. Puede hacer clic en la memoria caché en cualquiera de esos página de propiedades de ubicaciones tooopen hello de la memoria caché.

   ![Azure Portal][AZ04]

1. Cuando se muestra la página de Hola que contiene la lista de Hola de propiedades de la memoria caché, haga clic en **las claves de acceso** y copie las claves de acceso de la memoria caché.

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Crear una aplicación personalizada con hello Initializr primavera

1. Examinar demasiado<https://start.spring.io/>.

1. Especifique que desea toogenerate una **Maven** proyecto con **Java**, escriba Hola **grupo** y **Aritifact** nombres para la aplicación, y, a continuación, haga clic en el vínculo de hello demasiado**versión completa de conmutador toohello** de hello primavera Initializr.

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hola primavera Initializr usará hello **grupo** y **Aritifact** nombre del paquete de nombres toocreate Hola; por ejemplo: *com.contoso.myazuredemo*.
   >

1. Desplácese hacia abajo toohello **Web** y la sección de casilla hello para **Web**, a continuación, desplácese hacia abajo toohello **NoSQL** y la sección de casilla hello para **Redis**, a continuación, desplácese toohello inferior de la página de Hola y haga clic en botón Hola demasiado**generar proyecto**.

   ![Opciones completas de Spring Initializr][SI02]

1. Cuando se le solicite, descargue la ruta de acceso de hello proyecto tooa en el equipo local.

   ![Descarga del proyecto personalizado de Spring Boot][SI03]

1. Una vez extraídos los archivos de hello en el sistema local, la aplicación de arranque de primavera personalizada estará lista para su edición.

   ![Archivos de proyecto personalizados de Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Configure su toouse Spring arranque personalizado en la caché de Redis

1. Busque hello *application.properties* archivo Hola *recursos* directorio de la aplicación, o crear el archivo hello si aún no existe.

   ![Busque el archivo de hello application.properties][RE01]

1. Abra hello *application.properties* un archivo en un editor de texto y agregue Hola líneas toohello archivo siguiente y reemplace los valores de ejemplo de Hola con propiedades adecuadas de Hola desde la memoria caché:

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Editar archivo de hello application.properties][RE02]

1. Guarde y cierre hello *application.properties* archivo.

1. Cree una carpeta denominada *controlador* bajo la carpeta de origen de hello para el paquete; por ejemplo:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   O bien

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Crear un nuevo archivo denominado *HelloController.java* en hello *controlador* carpeta. Abra el archivo hello en un editor de texto y agregue Hola después tooit de código:

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
   
   Necesitará tooreplace `com.contoso.myazuredemo` con el nombre de paquete de hello para el proyecto.

1. Guarde y cierre hello *HelloController.java* archivo.

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Probar la aplicación web de hello examinando toohttp://localhost:8080 mediante un explorador web o utilizar una sintaxis de hello como Hola siguiente ejemplo, si tienes curl disponible:

   ```shell
   curl http://localhost:8080
   ```

   Debería ver Hola "¡Hello World!" del controlador de ejemplo mostrado, que se está recuperando dinámicamente de la memoria caché en Redis.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de las aplicaciones de arranque del muelle en Azure, vea Hola siguientes artículos:

* [Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Ejecuta una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].

Para obtener más información sobre cómo obtener iniciado con caché en Redis de Java en Azure, consulte [cómo toouse caché de Redis de Azure con Java][Redis Cache with Java].

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
