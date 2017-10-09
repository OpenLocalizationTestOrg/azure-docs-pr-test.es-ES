---
title: "aaaHow toowork con orígenes de datos de 'big data' | Documentos de Microsoft"
description: "Tooarticle cómo resaltados patrones para usar el catálogo de datos con orígenes de datos de 'big data', como almacenamiento de blobs de Azure y Azure Data Lake, Hadoop HDFS."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>Cómo orígenes toowork con grandes cantidades de datos en el catálogo de datos
## <a name="introduction"></a>Introducción
**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección de orígenes de datos empresariales. Son algo fundamental que ayuda a personas detectar, comprender y usar orígenes de datos y ayudar a las organizaciones tooget más valor de sus orígenes de datos existentes, incluidas grandes cantidades de datos.

**Catálogo de datos de Azure** admite Hola registro de blobs de almacenamiento de blobs de Azure y directorios, así como archivos de Hadoop HDFS y directorios. naturaleza semiestructurados de Hola de estos orígenes de datos proporciona gran flexibilidad. Sin embargo, tooget Hola mayor valor de su registro con **el catálogo de datos**, los usuarios deben tener en cuenta cómo se organizan los orígenes de datos de Hola.

## <a name="directories-as-logical-data-sets"></a>Directorios como conjuntos de datos lógicos
Un patrón común para organizar los orígenes de datos grandes es tootreat directorios como conjuntos de datos lógicos. Directorios de nivel superior son toodefine usa un conjunto de datos, mientras las subcarpetas definición particiones y archivos de Hola que contienen almacenan datos de hello propio.

Un ejemplo de este patrón puede ser:

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

En este ejemplo, vehicle_maintenance_events y location_tracking_events representan conjuntos de datos lógicos. Todas estas carpetas contienen archivos de datos que se organizan por año y mes en subcarpetas. Potencialmente, cada una de estas carpetas puede contener cientos o miles de archivos.

En este patrón, el registro de archivos individuales en **Catálogo de datos de Azure** probablemente no tenga sentido. En su lugar, registre los directorios de Hola que representan los conjuntos de datos de Hola que ser toohello significativa a los usuarios trabajar con datos de Hola.

## <a name="reference-data-files"></a>Archivos de datos de referencia
Un patrón complementario es toostore conjuntos de datos de referencia como archivos individuales. Estos conjuntos de datos puede considerarse como el lado de "pequeño" hello de grandes cantidades de datos y suelen ser toodimensions similar en un modelo de datos analíticos. Archivos de datos de referencia contienen registros de contexto tooprovide usado para cargas masivas de Hola Hola de archivos de datos almacenados en otras partes de almacén de datos grande de Hola.

Un ejemplo de este patrón puede ser:

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

Cuando científico de datos o analista se trabaja con datos de hello incluidos en estructuras de directorio de gran tamaño de hello, datos de hello en estos archivos de referencia pueden ser usado tooprovide información más detallada para las entidades que están mencionados tooonly por nombre o identificador de datos más grandes de Hola conjunto.

En este modelo, tiene sentido tooregister archivos de datos de referencia individual de hello con **el catálogo de datos**. Cada archivo representa un conjunto de datos y cada uno de ellos se puede anotar y detectar individualmente.

## <a name="alternate-patterns"></a>Patrones alternativos
patrones que se describen en la sección anterior de Hola Hola son sólo dos formas posibles de que un almacén de grandes cantidades de datos se puede organizar, pero cada implementación es diferente. Independientemente de cómo se estructuran los orígenes de datos, al registrar orígenes de datos grandes con **el catálogo de datos**, se centran en registrar Hola archivos y directorios que representan los conjuntos de datos de hello del valor tooothers dentro de su organización. Registrar todos los archivos y directorios puede abarrotar catálogo hello, lo que sea más difícil para los usuarios toofind lo necesitan.

## <a name="summary"></a>Resumen
Registrar orígenes de datos con **el catálogo de datos** hace que sea más fácil toodiscover y comprender. Mediante el registro y anotar Hola grandes cantidades de datos archivos y directorios que representan los conjuntos de datos lógicos, puede ayudar a los usuarios buscar y usar orígenes de datos grandes de Hola que necesitan.
