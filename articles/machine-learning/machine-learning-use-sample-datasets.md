---
title: "aaaUse conjuntos de datos de ejemplo de Hola en estudio de aprendizaje automático | Documentos de Microsoft"
description: "Descripciones de los conjuntos de datos de hello usados en los modelos de ejemplo incluidos en estudio de aprendizaje automático. Puede usar estos conjuntos de datos de ejemplo para los experimentos."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Usar conjuntos de datos de ejemplo de Hola en estudio de aprendizaje automático de Azure
[top]: #machine-learning-sample-datasets

Cuando se crea un área de trabajo nueva en Azure Machine Learning, de manera predeterminada se incluyen diversos conjuntos de datos y experimentos de ejemplo. Muchos de estos conjuntos de datos de ejemplo se utilizan en los modelos de ejemplo de Hola Hola [Galería de Azure de inteligencia Cortana](http://gallery.cortanaintelligence.com/). Otros se incluyen como ejemplos de distintos tipos de datos que se usan normalmente en el aprendizaje automático.

Algunos de estos conjuntos de datos están disponibles en Azure Blob Storage. Para estos conjuntos de datos, hello en la tabla siguiente proporciona un vínculo directo. Puede usar estos conjuntos de datos en sus experimentos mediante hello [importar datos] [ import-data] módulo.

resto de Hola de estos conjuntos de datos de ejemplo están disponibles en el área de trabajo en **conjuntos de datos guardados** en izquierda de hello módulo paleta toohello del lienzo del experimento de hello al abrir o crear un experimento de nuevo en estudio de aprendizaje automático.
Puede usar cualquiera de estos conjuntos de datos en su propia experimento arrastrando tooyour lienzo del experimento.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>Nombre del conjunto de datos</th>
  <th align=left>Descripción del conjunto de datos</th>
</tr>

<tr>
  <td valign=top>Conjunto de datos de clasificación binaria de ingresos en el censo de adultos</td>
  <td valign=top>
Un subconjunto de la base de datos de hello 1994 del censo, utilizando a los adultos de trabajo a través de la edad de Hola de 16 con un índice de ingresos ajustada de > 100.<p> </p><b>Uso:</b> clasificar personas que usan datos demográficos toopredict si una persona gana más de 50 K un año.<p> </p><b>Investigación relacionada:</b> Kohavi, R., Becker, B., (1996). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Conjunto de datos de códigos de aeropuerto</td>
  <td valign=top>
Códigos para aeropuertos de EE. UU.<p> </p>Este conjunto de datos contiene una fila por cada aeropuerto de Estados Unidos, proporcionar número de Id. de aeropuerto de Hola y el nombre junto con hello ubicación ciudad y estado.
  </td>
</tr>

<tr>
  <td valign=top>Información sobre los precios de los automóviles (datos sin procesar)</td>
  <td valign=top>
Obtener información acerca de automóviles por marca y modelo, incluido el precio de hello, características como el número de Hola de cilindros y MPG, así como una puntuación de riesgos de seguro.<p> </p>puntuación de riesgo de Hello inicialmente asociada precio automático y, a continuación, se ajusta de riesgo real en un proceso denominado tooactuaries como symboling. Un valor de + 3 indica que es arriesgado automática hello, y un valor de -3 que probablemente sea seguro.<p> </p><b>Uso:</b> puntuación de riesgo de hello Predict características, mediante la clasificación de regresión o multivariante. <p> </p><b>Investigación relacionada:</b> Schlimmer, J.C. (1987). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Conjunto de datos UCI de alquiler de bicicletas</td>
  <td valign=top>
Conjunto de datos UCI Bike Rental basados en datos reales tomados de la empresa Capital Bikeshare, que mantiene una red de alquiler de bicicletas en Washington DC.<p> </p>conjunto de datos de Hello tiene una fila para cada hora de cada día en 2011 y 2012, para un total de 17,379 filas. intervalo de Hola de alquiler de bicicletas por hora es de 1 too977.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Imagen RGB de Bill Gates</td>
  <td valign=top>
Archivo de imagen disponible públicamente convierte datos tooCSV.<p> </p>Hello para convertir la imagen de Hola se proporciona código de hello <strong>mediante la agrupación en clústeres K-Means de cuantificación del Color</strong> página de detalles del modelo.
  </td>
</tr>

<tr>
  <td valign=top>Datos sobre donación de sangre</td>
  <td valign=top>
Un subconjunto de datos de base de datos del donantes de sangre de Hola de hello transfusiones Service Center de Hsin Chu City, Taiwán.<p> </p>Datos de donantes incluyen meses Hola desde el último donación) y frecuencia u Hola número total de donaciones, tiempo transcurrido desde el último donación y cantidad de sangre dona.<p> </p><b>Uso:</b> objetivo de hello es toopredict a través de clasificación si donantes Hola donado sangre en marzo de 2007, donde 1 indica un donantes durante el período de destino de Hola y 0 un usuario que no donantes. <p> </p><b>Investigación relacionada:</b> Yeh, I.C., (2008). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  <p> </p>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence, "Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Reseñas de libros de Amazon</td>
  <td valign=top>
Revisiones de libros de Amazon, tomadas del sitio Web de amazon.com Hola por investigadores de la Universidad de Pensilvania (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">opiniones</a>). Vea el artículo de investigación de hello, "biografías, Bollywood, cuadros de auge y batidoras: adaptación de dominio para opiniones" John Blitzer, Mark Dredze y Fernando Pereira; Asociación de cálculo Linguistics (ACL) 2007.<p> </p>conjunto de datos original de Hello tiene revisiones de 975 K con clasificaciones 1, 2, 3, 4 o 5. Hola revisiones se han escrito en inglés y son de hello período 1997-2007. Este conjunto de datos ha sido muestrear abajo too10K revisiones.
  </td>
</tr>

<tr>
  <td valign=top>Datos sobre cáncer de mama</td>
  <td valign=top>
Uno de los tres conjuntos de relacionados con el ejemplo de cáncer de datos proporcionados por hello Institute oncológicos que aparece con frecuencia en la documentación de aprendizaje de máquina. Combina información de diagnóstico con características de análisis de laboratorio de unas 300 muestras de tejido.<p> </p><b>Uso:</b> clasificar tipo hello de ejemplo de cáncer, en función de 9 atributos, algunos de los cuales son lineales y algunos son de categorías. <p> </p><b>Investigación relacionada:</b> Wohlberg, W.H., Street, W.N., &amp; Mangasarian, O.L. (1995). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>Características de cáncer de mama <td valign=top>
Hola conjunto de datos contiene información para regiones sospechosos de 102K (candidatos) de imágenes de rayos x, cada uno de ellos descrito por 117 características. características de Hello son propietarios y su significado no se revele los creadores de conjunto de datos de hello (Siemens Healthcare). 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>Información sobre cáncer de mama</td>
  <td valign=top>
conjunto de datos de Hello contiene información adicional para cada región sospechosa de la imagen de rayos x. Cada ejemplo proporciona información (p. ej., etiqueta, paciente Id. de coordenadas de la imagen completa de revisión toohello relativa) acerca del número de fila correspondiente de hello en conjunto de datos de características de ejemplo de cáncer de mama Hola. Cada paciente tiene una serie de ejemplos. Para los pacientes con cáncer, algunos ejemplos son positivos y otros son negativos. Para los pacientes que no tienen cáncer, todos los ejemplos son negativos. conjunto de datos de Hello tiene ejemplos de 102K. se inclina Hola dataset, 0,6% de puntos de hello son positivas, rest Hola son negativos. conjunto de datos de Hola se puso a disposición mediante Siemens Healthcare.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>Etiquetas de apetencia CRM compartidas</td>
  <td valign=top>
Las etiquetas de desafío de predicción de relación de cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>Etiquetas de rotación de clientes de CRM compartidas</td>
  <td valign=top>
Las etiquetas de desafío de predicción de relación de cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>Conjunto de datos CRM compartido</td>
  <td valign=top>
Estos datos proceden de desafío de predicción de relación de cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>conjunto de datos de Hello contiene a clientes de 50K de hello empresa francés Telecom naranja. Cada cliente tiene 230 características anónimas, 190 de las cuales son numéricas y 40, categóricas. características de Hello están muy dispersos.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>Etiquetas de mejora de ventas de CRM compartidas</td>
  <td valign=top>
Las etiquetas de desafío de predicción de relación de cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Datos de regresión de eficiencia energética</td>
  <td valign=top>
Colección de perfiles energéticos simulados, con base en 12 formas de edificios diferentes. edificios de Hola se diferencian en 8 características, como cristal área, Hola cristal distribución de área y la orientación.<p> </p><b>Uso:</b> usar regresión o clasificación toopredict Hola eficacia energética de calificación basado en uno de dos respuestas con valores reales. Para la clasificación multiclase, es de ida y vuelta Hola respuesta variable toohello al entero más próximo. <p> </p><b>Investigación relacionada:</b> Xifara, A. &amp; Tsanas, A. (2012). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Datos de retrasos de vuelos</td>
  <td valign=top>
Vuelo acompañante en tiempo de los datos de rendimiento tomados de hello TranStats de recopilación de datos de hello EE. UU. de Transporte de EE.UU. (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">On-Time</a>).<p> </p>conjunto de datos de Hello abarca Hola abril-octubre de 2013 del período de tiempo. Antes de cargar tooAzure estudio de aprendizaje automático, el conjunto de datos de Hola se procesa del siguiente modo:<ul><li>conjunto de datos de Hello era toocover filtrado solo Hola 70 más ocupados aeropuertos continental Hola EE. UU.</li><li>Los vuelos cancelados se etiquetaron como retrasados más de 15 minutos.</li><li>Los vuelos desviados se quitaron de la muestra.</li><li>Hello columnas siguientes se seleccionaron: año, mes, DayofMonth, DayOfWeek, operador, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, Canceled</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Información sobre puntualidad de vuelos (datos sin procesar)</td>
  <td valign=top>
Registros de llegadas y salidas de aviones dentro de Estados Unidos desde octubre de 2011.<p> </p><b>Uso:</b> predecir retrasos en los vuelos. <p> </p><b>Investigación relacionada:</b> datos tomados del Departamento de Transporte de EE. UU. <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&amp;DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Datos de incendios forestales</td>
  <td valign=top>
Contiene información meteorológica (como índices de temperatura y humedad y velocidad del viento) de una zona del noreste de Portugal combinada con registros de incendios forestales.<p> </p><b>Uso:</b> esto es una tarea difícil de regresión, que el objetivo de hello toopredict Hola grabado área no cliente de incendio en el bosque. <p> </p><b>Investigación relacionada:</b> Cortez, P., &amp; Morais, A. (2008). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  <p> </p>[Cortez y Morais, 2007] P. Cortez y A. Morais. Un incendio en el bosque con datos meteorológicos de enfoque de minería de datos tooPredict. En J. Neves, M. F. Santos y J. Machado EDS, nuevas tendencias en Inteligencia Artificial, procedimientos de Hola 13 EPIA 2007 - portugués conferencia en Inteligencia Artificial, diciembre, Guimarães (Portugal), pp 512-523, 2007. APPIA, ISBN-13 978-989-95618-0-9. Disponible en: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>Conjunto de datos UCI de tarjeta de crédito alemana</td>
  <td valign=top>
Hola UCI Statlog (tarjeta de crédito alemana) conjunto de datos (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + alemán + crédito + datos</a>), mediante el archivo de hello german.data.<p> </p>conjunto de datos de Hello clasifica personas, descritas por un conjunto de atributos, como los riesgos de crédito baja o alta. Cada ejemplo representa a una persona. Hay 20 características, numéricos y de categorías y una etiqueta binaria (valor de riesgo de crédito de hello). Las partidas de riesgo de crédito alto tienen la etiqueta = 2, mientras que las partidas con riesgo de crédito bajo tienen la etiqueta = 1. costo de Hola de clasifique mal un ejemplo de bajo riesgo tan alto es 1, mientras que el costo de Hola de clasifique mal un ejemplo de alto riesgo como baja es 5.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>Títulos de películas en IMDB</td>
  <td valign=top>
Hello conjunto de datos contiene información sobre las películas que se han clasificado en Twitter tweets: IMDB Id. de la película, el nombre de la película, género y año de producción. Hay 17K películas en el conjunto de datos de Hola. conjunto de datos de Hola se introdujo en papel de Hola "S. Dooms, T. De Pessemier y L. Martens. MovieTweetings: un conjunto de datos sobre valoración de películas recopilado de Twitter. Taller de micromecenazgo y cálculo humano para sistemas de recomendación, CrowdRec en RecSys 2013."
  </td>
</tr>

<tr>
  <td valign=top>Datos sobre iris de dos clases</td>
  <td valign=top>
Se trata quizás de hello más conocido toobe de base de datos que se encuentra en la documentación de reconocimiento de patrón de Hola. conjunto de datos de Hello es relativamente pequeño, que contiene 50 ejemplos de mediciones de pétalo de tres variedades de iris.<p> </p><b>Uso:</b> predecir Hola iris tipo de mediciones de Hola.  <p> </p><b>Investigación relacionada:</b> Fisher, R.A. (1988). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Tweets sobre películas</td>
  <td valign=top>
conjunto de datos de Hello es una versión extendida del conjunto de datos de película Tweetings Hola. conjunto de datos de Hello tiene 170K clasificaciones de películas, extraídos de tweets estructurados en Twitter. Cada instancia representa un tweet y es una tupla: Id. de usuario, Id. de película IMDB, valoración, marca de tiempo, número de favoritos para ese tweet y número de retweets de ese tweet. conjunto de datos de Hola se proporcionada por dice A., S. Dooms, B. Loni y D. Tikk de 2014 de desafío de sistemas de recomendación.
  </td>
</tr>

<tr>
  <td valign=top>Datos sobre consumo de combustible por distancia recorrida para varios automóviles</td>
  <td valign=top>
Este conjunto de datos es una versión ligeramente modificada del conjunto de datos de hello proporcionada por hello StatLib biblioteca de la Universidad Carnegie Mellon. conjunto de datos de Hola se usó en hello 1983 American exposición estadística de asociación.<p> </p>Hola datos presentan el consumo de combustible para varios automóviles en kilómetros por litro, junto con información como un número de cilindros, desplazamiento de motor, potencia, peso total y aceleración Hola.<p> </p><b>Uso:</b> predecir el ahorro de combustible en función de tres atributos discretos multivalor y cinco atributos continuos. <p> </p><b>Investigación relacionada:</b> StatLib, Carnegie Mellon University, (1993). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  </td>
</tr>

<tr>
  <td valign=top>Conjunto de datos de clasificación binaria sobre diabetes en indios pima</td>
  <td valign=top>
Un subconjunto de datos de base de datos de hello Instituto nacional de Diabetes y digestivo y riñones enfermedades. conjunto de datos de Hello era toofocus filtrados en pacientes femeninos de patrimonio India Pima. Hola se incluyen datos médicos como glucosa y niveles de insulina, así como factores de estilo de vida.<p> </p><b>Uso:</b> predecir si el asunto de hello tiene diabetes (clasificación binaria). <p> </p><b>Investigación relacionada:</b> Sigillito, V. (1990). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  </td>
</tr>

<tr>
  <td valign=top>Datos de clientes de restaurantes</td>
  <td valign=top>
Conjunto de metadatos sobre clientes que incluye información demográfica y preferencias.<p> </p><b>Uso:</b> usar este conjunto de datos, en combinación con Hola otros conjuntos de datos de dos restaurante, tootrain y probar un sistema de recomendación. <p> </p><b>Investigación relacionada:</b> Bache, K. y Lichman, M. (2013). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información
  </td>
</tr>

<tr>
  <td valign=top>Datos de características de restaurantes</td>
  <td valign=top>
Un conjunto de metadatos acerca de restaurantes y sus características, como el tipo de comida, el estilo de comedor y la ubicación.<p> </p><b>Uso:</b> usar este conjunto de datos, en combinación con Hola otros conjuntos de datos de dos restaurante, tootrain y probar un sistema de recomendación. <p> </p><b>Investigación relacionada:</b> Bache, K. y Lichman, M. (2013). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información
  </td>
</tr>

<tr>
  <td valign=top>Valoraciones de restaurantes</td>
  <td valign=top>
Contiene las clasificaciones proporcionadas por los usuarios toorestaurants en una escala desde too2 0.<p> </p><b>Uso:</b> usar este conjunto de datos, en combinación con Hola otros conjuntos de datos de dos restaurante, tootrain y probar un sistema de recomendación. <p> </p><b>Investigación relacionada:</b> Bache, K. y Lichman, M. (2013). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información
  </td>
</tr>

<tr>
  <td valign=top>Conjunto de datos de varias clases de recocido de acero</td>
  <td valign=top>
Este conjunto de datos contiene una serie de registros de acero recocido evaluaciones con atributos físicos de hello (ancho, espesor, tipos de tipo (resorte, hoja, etc.) de hello resultante acero.<p> </p><b>Uso:</b> predecir cualquiera de los dos atributos de clase numéricos: rigidez o solidez. También puede analizar las correlaciones entre atributos.<p> </p>Los grados del acero siguen una norma establecida, definida por la SAE y otras organizaciones. Busca un determinado 'grado de (variable de clase hello) y desea que los valores de hello toounderstand necesarios. <p> </p><b>Investigación relacionada:</b> Sterling, D. &amp; Buntine, W., (NA). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información  <p> </p>Un grados de toosteel guía útil pueden encontrarse aquí: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Datos de telescopio</td>
  <td valign=top>
Registro de explosiones de partículas gamma de alta energía junto con ruido de fondo, ambos simulados utilizando un proceso de Monte Carlo.<p> </p>intención de Hola de simulación de hello era tooimprove precisión de Hola de tierra atmosférica Cherenkov gamma telescopios, mediante métodos estadísticos toodifferentiate entre señal deseada de hello (Cherenkov radiación duchas) y el ruido de fondo (hadronic duchas iniciadas por rayos cósmicos en hello superior ambiente).<p> </p>Hello datos ha sido toocreate preprocesado un clúster alargado con eje longitudinal Hola se orientan hacia el centro de la cámara de Hola. características de Hola de esta elipse (también denominados Hillas parámetros) se encuentran entre parámetros de imagen de Hola que pueden usarse para la distinción.<p> </p><b>Uso:</b> predecir si la imagen de una ducha representa señal o ruido de fondo.<p> </p><b>Notas:</b> la precisión de clasificación sencilla no es significativa para estos datos, ya que clasificar un evento de fondo como señal es peor que clasificar un evento de señal como fondo. Para la comparación de clasificadores diferentes gráfico de hello ROC debe utilizarse. Hola probabilidad de aceptar un evento en segundo plano como señal debe ser inferior a alguno de hello después de umbrales: 0,01, 0,02, 0,05, 0,1 o 0,2.<p> </p>Además, tenga en cuenta que es infravaloró número Hola de eventos de fondo (de duchas hadronic, h), mientras que en medidas reales, clase h o ruido de hello representa la mayoría de Hola de eventos. <p> </p><b>Investigación relacionada:</b> Bock, R.K. (1995). Repositorio de aprendizaje automático de UCI <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: Universidad de California, Facultad de Ciencias de la Computación y de la Información </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Conjunto de datos del tiempo</td>
  <td valign=top>
Cada hora observaciones de tiempo terrestres de NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">combinan datos de too201310 201304</a>).<p> </p>los datos del tiempo Hola cubren las observaciones realizadas desde estaciones meteorológicas de aeropuerto, que abarcan Hola abril-octubre de 2013 del período de tiempo. Antes de cargar tooAzure estudio de aprendizaje automático, el conjunto de datos de Hola se procesa del siguiente modo:<ul><li>Id. de estación meteorológica fueron asignadas toocorresponding aeropuerto identificadores</li><li>Se filtran estaciones meteorológicas no esté asociadas a aeropuertos de más ocupados 70 Hola</li><li>columna de fecha de Hola se dividió en columnas independientes de año, mes y día</li><li>Hello columnas siguientes se seleccionaron: AirportID, año, mes, día, hora, zona horaria, SkyCondition, visibilidad, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, Velocidad del viento, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, Tiporegistro, HourlyPrecip, altímetro</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Conjunto de datos de SP 500 de Wikipedia</td>
  <td valign=top>
Los datos se han extraído de Wikipedia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) y se basan en artículos de cada empresa del índice S&P 500, almacenados como datos XML.<p> </p>Antes de cargar tooAzure estudio de aprendizaje automático, el conjunto de datos de Hola se procesa del siguiente modo:<ul><li>Se extrajo el contenido de texto para cada empresa específica.</li><li>Se eliminó el formato wiki.</li><li>Se eliminaron los caracteres no alfanuméricos</li><li>Convertir todos los toolowercase de texto</li><li>Se agregaron las categorías de empresas conocidas.</li></ul><p> </p>Tenga en cuenta que para algunas empresas un artículo no se pudo encontrar, por lo que el número de Hola de registros es menor que 500.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
conjunto de datos de Hello contiene los datos del cliente e indicaciones sobre su campaña de correo directo de tooa de respuesta. Cada fila representa a un cliente. conjunto de datos Hello contiene 9 características sobre datos demográficos de los usuarios y más allá de comportamiento y 3 columnas de etiqueta (visite, conversión y dedicar).  Visita es una columna binaria que indica que un cliente visitado después de hello campaña de marketing, conversión indica un cliente adquirió algo y dedicar es la cantidad de Hola que se dedicó a.  conjunto de datos de Hola se puso a disposición por Kevin Hillstrom para MineThatData correo electrónico análisis de comprobación y de datos de minería de datos.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Características de los ejemplos de prueba en el conjunto de datos de hello RCV1 V2 Reuters noticias. conjunto de datos de Hello tiene 781K nuevos artículos junto con sus identificadores (primera columna del conjunto de datos de hello). Los artículos están acortados, excluyen palabras reservadas y su contenido se reduce a la raíz de cada palabra. conjunto de datos de Hola se puso a disposición por David. D. Lewis.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Características de ejemplos de entrenamiento en el conjunto de datos de hello RCV1 V2 Reuters noticias. conjunto de datos de Hello tiene 23K nuevos artículos junto con sus identificadores (primera columna del conjunto de datos de hello). Los artículos están acortados, excluyen palabras reservadas y su contenido se reduce a la raíz de cada palabra. conjunto de datos de Hola se puso a disposición por David. D. Lewis.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
Conjunto de datos de hello KDD Cup 1999 la detección de conocimiento y competencia de herramientas de minería de datos (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>conjunto de datos de Hola se descargó y almacenado en el almacenamiento de blobs de Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) e incluye el entrenamiento y conjuntos de datos de pruebas. conjunto de datos de entrenamiento de Hello tiene aproximadamente 126K filas y 43 columnas, incluidas las etiquetas de Hola. Tres columnas forman parte de la información de etiqueta de Hola y 40 columnas, que consta de las características de numéricos y de cadena/categoría, están disponibles para entrenar el modelo de Hola. datos de prueba de Hello tienen aproximadamente 22,5 K ejemplos con columnas de hello 43 mismo como en los datos de entrenamiento de Hola de prueba.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></td>
  <td valign=top>
Asignaciones de tema para los artículos de noticias en el conjunto de datos de hello RCV1 V2 Reuters noticias. Un artículo de noticias puede asignarse tooseveral temas. formato de Hola de cada fila es "&lt;el nombre del tema&gt; &lt;identificador de documento&gt; 1". conjunto de datos de Hello contiene las asignaciones de tema de 2,6 M. conjunto de datos de Hola se puso a disposición por David. D. Lewis.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Estos datos proceden de hello desafío de evaluación del rendimiento de KDD Cup 2010 estudiante (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">evaluación del rendimiento de estudiantes</a>). datos que se usan Hello están conjunto de entrenamiento de hello Algebra_2008_2009 (autor de la marca, J., Niculescu-Mizil, r., Ritter, S., Gordon, G.J. & Koedinger, j (2010). Álgebra I 2008-2009. Conjunto de datos obtenidos de la minería de datos educativos de KDD Cup 2010. Puede encontrarlos en <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> o <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>conjunto de datos de Hola se descargó y almacenado en el almacenamiento de blobs de Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) y contiene archivos de registro de un estudiante clases particulares de sistema. características de Hello proporcionado incluyen Id. del problema y su descripción breve, Id. de estudiante, marca de tiempo, y cuántos intentos de estudiante Hola realizado antes de solucionar el problema Hola Hola manera correcta. conjunto de datos original de Hello tiene registros de 8,9 M; Este conjunto de datos ha sido muestrear abajo toohello primeras filas de 100 KB. conjunto de datos de Hello tiene 23 columnas separados por tabulaciones de distintos tipos: numérico, categoría y marca de tiempo.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
