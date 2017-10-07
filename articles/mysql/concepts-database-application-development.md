---
title: "información general sobre el desarrollo de aplicaciones de aaaDatabase de base de datos de Azure para MySQL | Documentos de Microsoft"
description: "Presenta consideraciones de diseño que debería seguir un programador al escribir aplicaciones código tooconnect tooAzure base de datos de MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Introducción al desarrollo de aplicaciones para Azure Database for MySQL 
En este artículo se describe las consideraciones de diseño que debería seguir un programador al escribir aplicaciones código tooconnect tooAzure base de datos de MySQL 

> [!TIP]
> Encontrará un tutorial que se muestra cómo toocreate un servidor, se crea un firewall basado en servidor, ver propiedades del servidor, crea base de datos, conectarse y consulta mediante el área de trabajo y mysql.exe, [diseñar la primera base de datos de MySQL de Azure](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Plataforma y lenguaje
Existen ejemplos de código para diferentes lenguajes de programación y plataformas. Puede encontrar vínculos toohello ejemplos de código en: [bibliotecas de conectividad usan tooconnect tooAzure base de datos de MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Herramientas
Base de datos de Azure para MySQL usa la versión de comunidad de MySQL hello, compatible con MySQL de herramientas de administración habituales, tales como las utilidades de Workbench o MySQL como mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)y otros. También puede usar Hola portal de Azure, CLI de Azure y las API de REST toointeract con el servicio de base de datos de Hola.

## <a name="resource-limitations"></a>Limitaciones de recursos
La base de datos de MySQL Azure administra Hola recursos disponibles tooa server mediante dos mecanismos diferentes: 
- Gobierno de recursos 
- Aplicación de límites

## <a name="security"></a>Seguridad
La base de datos MySQL de Azure proporciona recursos para limitar el acceso, proteger los datos, configurar usuarios y roles y supervisar las actividades en una base de datos MySQL.

## <a name="authentication"></a>Autenticación
La base de datos MySQL de Azure admite la autenticación de servidor de usuarios e inicios de sesión.

## <a name="resiliency"></a>Resistencia
Cuando se produce un error transitorio al conectar tooMySQL base de datos, el código debe reintentar la llamada de Hola. Te recomendamos que uses Hola Reintentar lógica de interrupción lógica, por lo que no desborda Hola base de datos de SQL con varios clientes reintentando simultáneamente.

- Ejemplos de código: para los ejemplos de código que muestran la lógica de reintento, vea los ejemplos para el idioma de Hola de su elección en: [bibliotecas de conectividad usan tooconnect tooAzure base de datos de MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Administración de conexiones
Las conexiones de base de datos son un recurso limitado, por lo que te recomendamos que uses significativo de conexiones al obtener acceso a la base de datos de MySQL tooachieve un mejor rendimiento.
- Base de datos Access hello mediante la agrupación de conexiones o conexiones persistentes.
- Base de datos de Hola de Access mediante el uso de la duración de derivación. 
- Lógica de reintento de uso en la aplicación en el momento de Hola de intento de conexión de hello, toocatch errores debido a las conexiones tooconcurrent ha alcanzado el máximo de hello permitido. Hola lógica de reintento, establezca un breve retraso y, a continuación, espere durante un tiempo aleatorio antes de intentos de conexión adicionales de Hola.
