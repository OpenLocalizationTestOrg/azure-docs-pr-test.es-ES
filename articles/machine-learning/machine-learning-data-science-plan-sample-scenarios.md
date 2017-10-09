---
title: "aaaIdentify avanzada escenarios de análisis para el aprendizaje automático de Azure | Documentos de Microsoft"
description: "Seleccione escenarios adecuados de Hola para hacerlo avanzado análisis predictivos con hello proceso de ciencia de datos de equipo."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Escenarios para análisis avanzado en Aprendizaje automático de Azure
En este artículo se describe diversas Hola de orígenes de datos de ejemplo y escenarios de destino que pueden ser controlados por hello [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md). Hola TDSP proporciona un enfoque sistemático para toocollaborate de los equipos en la creación de aplicaciones inteligentes. escenarios de Hello proporcionados en esta guía ilustran opciones disponibles en el flujo de trabajo de procesamiento de datos de Hola que dependen de las características de datos de hello, ubicaciones de origen y destino repositorios en Azure.

Hola **árbol de decisión** para escenarios de ejemplo de Hola que sea adecuada para los datos y el objetivo de selección se presenta en la última sección de Hola.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Cada una de las siguientes secciones de hello presenta un escenario de ejemplo. Para cada escenario, se enumera un posible flujo de ciencia de datos y análisis avanzado, así como los recursos de compatibilidad de Azure.

> [!NOTE]
> **Para todos los escenarios siguientes de hello, necesitará:**
> <br/>
> 
> * [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Escenario \#1: toomedium pequeño conjunto de datos tabular en un archivos locales
![Archivos locales toomedium pequeño][1]

#### <a name="additional-azure-resources-none"></a>Recursos adicionales de Azure: ninguno
1. Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).
2. Cargue un conjunto de datos.
3. Cree un flujo de experimento de Aprendizaje automático de Azure comenzando con conjuntos de datos cargados.

## <a name="smalllocalprocess"></a>Escenario \#2: toomedium pequeño conjunto de datos de los archivos locales que requieren un procesamiento
![Toomedium pequeños archivos locales con el procesamiento][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Recursos adicionales de Azure: Máquina virtual de Azure (servidor IPython Notebook)
1. Cree una máquina virtual de Azure que ejecute IPython Notebook.
2. Cargar el contenedor de almacenamiento de Azure de tooan de datos.
3. Preprocese y limpie datos en IPython Notebook obteniendo acceso desde el contenedor de almacenamiento de Azure.
4. Transformar datos toocleaned, un formato tabular.
5. Guarde los datos transformados en blobs de Azure.
6. Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).
7. Leer datos de Hola de blobs de Azure mediante hello [importar datos] [ import-data] módulo.
8. Cree un flujo de experimento de Aprendizaje automático de Azure comenzando con conjuntos de datos introducidos.

## <a name="largelocal"></a>Escenario \#3: Conjunto de datos grande de archivos locales, con blobs de Azure como destino
![Archivos locales grandes][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Recursos adicionales de Azure: Máquina virtual de Azure (servidor IPython Notebook)
1. Cree una máquina virtual de Azure que ejecute IPython Notebook.
2. Cargar el contenedor de almacenamiento de Azure de tooan de datos.
3. Preprocese y limpie datos en IPython Notebook obteniendo acceso desde blobs de Azure.
4. Transformar datos toocleaned, formato tabular, si es necesario.
5. Explore datos y cree características según sea necesario.
6. Extraiga una muestra de datos de tamaño pequeño a medio.
7. Guardar datos de hello muestreada en blobs de Azure.
8. Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).
9. Leer datos de Hola de blobs de Azure mediante hello [importar datos] [ import-data] módulo.
10. Cree un flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos ingeridos.

## <a name="smalllocaltodb"></a>Escenario \#4: toomedium pequeño conjunto de datos de archivos locales, como el destino de SQL Server en una máquina Virtual de Azure
![Toomedium pequeños archivos locales tooSQL base de datos de Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)
1. Cree una máquina virtual de Azure que ejecute SQL Server + IPython Notebook.
2. Cargar el contenedor de almacenamiento de Azure de tooan de datos.
3. Preprocese y limpie datos en el contenedor de almacenamiento de Azure usando IPython Notebook.
4. Transformar datos toocleaned, formato tabular, si es necesario.
5. Guardar archivos de datos local de tooVM (Bloc de notas de IPython se ejecuta en máquinas virtuales, las unidades locales, consulte tooVM unidades).
6. Carga datos tooSQL base de datos Server ejecuta en una VM de Azure.
   
   Opción \#1: Mediante SQL Server Management Studio.
   
   * Inicio de sesión tooSQL máquina virtual Server
   * Ejecute SQL Server Management Studio.
   * Cree tablas de base de datos y de destino.
   * Use uno de forma masiva de Hola importar datos de Hola de tooload de métodos de archivos de máquina virtual local.
   
   Opción \#2: Mediante IPython Notebook (no se recomienda para conjuntos de datos de tamaño medio o más grandes)
   
   <!-- -->    
   * Usar tooaccess de cadena de conexión de ODBC SQL Server en máquina virtual.
   * Cree tablas de base de datos y de destino.
   * Use uno de forma masiva de Hola importar datos de Hola de tooload de métodos de archivos de máquina virtual local.
7. Explore datos y cree características según sea necesario. Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola. Tenga en cuenta solo Hola consulta necesarios toocreate ellos.
8. Elija un tamaño de muestra de datos, si lo necesita y/o desea.
9. Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).
10. Datos de lectura Hola directamente de Hola a SQL Server mediante hello [importar datos] [ import-data] módulo. Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.
11. Cree un flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos ingeridos.

## <a name="largelocaltodb"></a>Escenario \#5: Conjunto de datos grande de archivos locales, con SQL Server en una máquina virtual de Azure como destino
![Archivos locales grandes tooSQL base de datos de Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)
1. Cree una máquina virtual de Azure que ejecute SQL Server y el servidor IPython Notebook.
2. Cargar el contenedor de almacenamiento de Azure de tooan de datos.
3. (Opcional) Preprocese y limpie los datos.
   
   a.  Preprocese y limpie datos en IPython Notebook obteniendo acceso desde Azure
   
       blobs.
   
   b.  Transformar datos toocleaned, formato tabular, si es necesario.
   
   c.  Guardar archivos de datos local de tooVM (Bloc de notas de IPython se ejecuta en máquinas virtuales, las unidades locales, consulte tooVM unidades).
4. Carga datos tooSQL base de datos Server ejecuta en una VM de Azure.
   
   a.  TooSQL máquina virtual del servidor de inicio de sesión.
   
   b.  Si los datos todavía no están guardados, descargue los archivos de datos desde Azure
   
       storage container toolocal-VM folder.
   
   c.  Ejecute SQL Server Management Studio.
   
   d.  Cree tablas de base de datos y de destino.
   
   e.  Use uno de forma masiva de Hola importarlos métodos tooload Hola.
   
   f.  Si se necesitan combinaciones de tablas, crear combinaciones de tooexpedite de índices.
   
   > [!NOTE]
   > Para acelerar la carga de tamaños de datos de gran tamaño, se recomienda que cree tablas con particiones y datos de Hola de importación en paralelo de forma masiva. Para obtener más información, consulte [tooSQL de importación de datos paralelos Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Explore datos y cree características según sea necesario. Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola. Tenga en cuenta solo Hola consulta necesarios toocreate ellos.
6. Elija un tamaño de muestra de datos, si lo necesita y/o desea.
7. Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).
8. Datos de lectura Hola directamente de Hola a SQL Server mediante hello [importar datos] [ import-data] módulo. Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.
9. Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados

## <a name="largedbtodb"></a>Escenario \#6: Conjunto de datos grande de archivos locales, con SQL Server en una máquina virtual de Azure como destino
![Gran base de datos SQL local tooSQL base de datos de Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)
1. Cree una máquina virtual de Azure que ejecute SQL Server y el servidor IPython Notebook.
2. Use uno de los datos de hello exportarlos métodos tooexport Hola desde archivos toodump de SQL Server.
   
   > [!NOTE]
   > Si decide toomove todos los datos de base de datos de hello local, una alternativa (más rápido) método toomove Hola completa de la base de datos toothe instancia de SQL Server en Azure. Omitir pasos de hello tooexport datos, crear base de datos y base de datos de destino de carga/importar datos toohello y siga método alternativo de Hola.
   > 
   > 
3. Cargar el contenedor de almacenamiento de tooAzure de archivos de volcado de memoria.
4. Carga Hola datos tooa base datos SQL Server ejecuta en una máquina Virtual de Azure.
   
   a.  Inicio de sesión toohello VM de SQL Server.
   
   b.  Descargar archivos de datos desde una carpeta de local-VM de toohello de contenedor de almacenamiento de Azure.
   
   c.  Ejecute SQL Server Management Studio.
   
   d.  Cree tablas de base de datos y de destino.
   
   e.  Use uno de forma masiva de Hola importarlos métodos tooload Hola.
   
   f.  Si se necesitan combinaciones de tablas, crear combinaciones de tooexpedite de índices.
   
   > [!NOTE]
   > Para acelerar la carga de tamaños de datos de gran tamaño, crear tablas con particiones y toobulk importar datos de hello en paralelo. Para obtener más información, consulte [tooSQL de importación de datos paralelos Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Explore datos y cree características según sea necesario. Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola. Tenga en cuenta solo Hola consulta necesarios toocreate ellos.
6. Elija un tamaño de muestra de datos, si lo necesita y/o desea.
7. Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).
8. Datos de lectura Hola directamente de Hola a SQL Server mediante hello [importar datos] [ import-data] módulo. Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.
9. Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Método alternativo toocopy una base de datos completa de un tooAzure de SQL Server local base de datos SQL
![Base de datos local de separar y adjuntar tooSQL base de datos de Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)
tooreplicate Hola SQL Server base de datos completa en la VM de SQL Server, debe copiar una base de datos de una tooanother/servidor de ubicación, suponiendo que esa base de datos de Hola se pueden desconectar temporalmente. Para ello, en hello Explorador de objetos de SQL Server Management Studio, o mediante comandos de Transact-SQL equivalentes Hola.

1. Separar base de datos de hello en la ubicación de origen de Hola. Para más información, consulte [Desasociar una base de datos](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. En la ventana del explorador de Windows o el símbolo del sistema de Windows, Hola copia separa el archivo de base de datos o archivos y archivo de registro o ubicación de destino de archivos toohello en hello VM de SQL Server en Azure.
3. Asociar instancia de SQL Server de destino de hello copian archivos toohello. Para más información, consulte [Asociar una base de datos](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Mover una base de datos mediante las opciones desasociación y asociación (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Escenario \#7: Big Data de archivos locales, con base de datos de Hive como destino en clústeres de Hadoop de Azure HDInsight
![Datos de gran tamaño en Hive de destino local][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Recursos adicionales de Azure: Clúster de Hadoop de HDInsight de Azure y máquina virtual de Azure (servidor IPython Notebook)
1. Cree una máquina virtual de Azure que ejecute el servidor IPython Notebook.
2. Cree un clúster de Hadoop de HDInsight de Azure.
3. (Opcional) Preprocese y limpie los datos.
   
   a.  Preprocese y limpie datos en IPython Notebook obteniendo acceso desde Azure
   
       blobs.
   
   b.  Transformar datos toocleaned, formato tabular, si es necesario.
   
   c.  Guardar archivos de datos local de tooVM (Bloc de notas de IPython se ejecuta en máquinas virtuales, las unidades locales, consulte tooVM unidades).
4. Cargar el contenedor de datos toohello predeterminado del clúster de Hadoop de hello seleccionado en el paso 2 de Hola.
5. Carga datos tooHive base de datos en clúster de HDInsight Hadoop de Azure.
   
   a.  Inicie sesión en toohello nodo principal del clúster de Hadoop de Hola
   
   b.  Abra Hola línea de comandos de Hadoop.
   
   c.  Escriba el directorio de raíz del subárbol de hello comando `cd %hive_home%\bin` en línea de comandos de Hadoop.
   
   d.  Ejecutar la base de datos toocreate consultas de Hive de Hola y tablas y cargar datos de tablas de tooHive de almacenamiento de blobs.
   
   > [!NOTE]
   > Si los datos de hello están grandes, los usuarios pueden crear tabla de Hive Hola con particiones. A continuación, los usuarios pueden utilizar un `for` bucle en la línea de comandos de Hadoop de hello en los datos de tooload de nodo principal de hello en tabla de Hive Hola particionado por partición.
   > 
   > 
6. Explore datos y cree características según sea necesario en la línea de comandos de Hadoop. Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola. Tenga en cuenta solo Hola consulta necesarios toocreate ellos.
   
   a.  Inicie sesión en toohello nodo principal del clúster de Hadoop de Hola
   
   b.  Abra Hola línea de comandos de Hadoop.
   
   c.  Escriba el directorio de raíz del subárbol de hello comando `cd %hive_home%\bin` en línea de comandos de Hadoop.
   
   d.  Ejecutar consultas de Hive hello en línea de comandos de Hadoop en el nodo principal de Hola Hola Hadoop tooexplore Hola de datos de clúster y crear características según sea necesario.
7. Si necesita y/o deseado, ejemplo de Hola datos toofit en estudio de aprendizaje automático de Azure.
8. Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).
9. Leer datos de hello directamente desde hello `Hive Queries` con hello [importar datos] [ import-data] módulo. Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.
10. Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados.

## <a name="decisiontree"></a>Árbol de decisión de selección de escenario
- - -
Hello diagrama siguiente resume escenarios Hola que se ha descrito anteriormente y opciones proceso de análisis avanzado y la tecnología de hello elegido que toman tooeach de escenarios de hello detallado. Tenga en cuenta que pueden llevar a cabo el procesamiento de datos, la exploración, ingeniería de característica y muestreo colocar en uno o más entornos de destino, o método/entorno--en origen hello, intermedio y puede realizarse de forma iterativa según sea necesario. diagrama de Hello solo sirve para ilustrar algunos de los flujos de posibles y no proporciona una enumeración exhaustiva.

![Escenarios de tutoriales de proceso de ciencia de datos de ejemplo][8]

### <a name="advanced-analytics-in-action-examples"></a>Ejemplos de análisis avanzado en acción
Para ver tutoriales de aprendizaje automático de Azure de extremo a extremo que emplean Hola tecnología y el proceso de análisis avanzado mediante conjuntos de datos públicas, vea:

* [Proceso de ciencia de datos en equipos en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Proceso de ciencia de datos en equipos en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md)

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
