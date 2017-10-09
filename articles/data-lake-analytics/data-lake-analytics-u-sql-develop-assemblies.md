---
title: "ensamblados de aaaDevelop U-SQL para trabajos de análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se usa y reutiliza en los análisis de Data Lake trabajos toodevelop ensamblados toobe. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics
Obtenga información acerca de cómo tooturn código subyacente en ensamblados toobe usa y volver a usar en trabajos de análisis de Data Lake. 

U-SQL hace fácil tooadd su propio personalizado de código en lenguajes. NET, como C#, Visual Basic.NET o F #. Incluso puede implementar su propio toosupport en tiempo de ejecución de otros lenguajes.

código personalizado de Hello más fácil manera toouse es toouse hello Data Lake Tools para capacidades de código subyacente de Visual Studio. Para obtener más información, consulte [Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Sin embargo, usar código subyacente tiene algunas desventajas:

- código fuente de Hello obtiene cargado para el envío de cada secuencia de comandos.
- El código subyacente no se puede compartir con otros trabajos.

tooaddress estas desventajas, puede convertir el código subyacente en ensamblados y registrar el catálogo de análisis de Data Lake de hello ensamblados toohello.

## <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 Update 4 o Visual Studio 2012 con Visual C ++ Instalado
* SDK de Microsoft Azure para .NET versión 2.5 o posterior.  Instalar mediante el instalador de plataforma Web de Hola o instalador de Visual Studio
* Una cuenta de Análisis de Data Lake.  [Introducción a Azure Data Lake Analytics mediante Azure Portal](data-lake-analytics-get-started-portal.md).
* Vaya a través de hello [empezar a trabajar con Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.
* Conectar tooAzure.
* Cargar datos de origen de hello, consulte [empezar a trabajar con Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Desarrollo de ensamblados para U-SQL

**toocreate y enviar un trabajo de SQL U**

1. De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.
2. Expanda **instalado**, **plantillas**, **Azure Data Lake**, **U-SQL(ADLA)**, seleccione hello **biblioteca de clases (para U-SQL Aplicación)** plantilla y, a continuación, haga clic en **Aceptar**.
3. Escriba el código en Class1.cs.  Hola aquí te mostramos un ejemplo de código.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Haga clic en hello **generar** menú y, a continuación, haga clic en **generar solución** toocreate Hola dll.

## <a name="register-assemblies"></a>Registro de ensamblados

Consulte [Uso del catálogo de Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Usar ensamblados de Hola

Vea [usar hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>Otras referencias
* [Introducción a Análisis de Data Lake mediante PowerShell](data-lake-analytics-get-started-powershell.md)
* [Empezar a trabajar con análisis de Data Lake con hello portal de Azure](data-lake-analytics-get-started-portal.md)
* [Uso de Data Lake Tools for Visual Studio para desarrollar aplicaciones de U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
* [Uso del catálogo de Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md)
* [Usar hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
