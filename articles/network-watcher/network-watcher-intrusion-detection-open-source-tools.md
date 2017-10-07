---
title: "aaaPerform la detección de intrusiones de red con Monitor de red de Azure y herramientas de código abierto | Documentos de Microsoft"
description: "Este artículo describe cómo toouse Monitor de red de Azure y código abierto herramientas tooperform la detección de intrusiones de red"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Realización de detección de intrusiones en la red con Azure Network Watcher y herramientas de código abierto

Las capturas de paquetes son un componente clave de la implementación de sistemas de detección de intrusiones de red (IDS) y de la ejecución de supervisión de seguridad de la red (NSM). Existen varias herramientas IDS de código abierto que procesan las capturas de paquetes y buscan firmas de posibles intrusiones y actividad malintencionada. Con capturas de paquetes de saludo proporcionadas por el Monitor de red, puede analizar la red en busca de vulnerabilidades ni las intrusiones perjudiciales.

Una de estas herramientas de código abierto es Suricata, un motor de identificadores que usa el tráfico de red de rulesets toomonitor y desencadena alertas cuando se producen eventos sospechosos. Suricata ofrece un motor multiproceso, lo que significa que puede realizar el análisis del tráfico de red con una mayor velocidad y eficiencia. Para más información sobre Suricata y sus funcionalidades, visite este sitio web en https://suricata-ids.org/.

## <a name="scenario"></a>Escenario

Este artículo explica cómo tooset una tooperform de su entorno mediante el Monitor de red, Suricata, la detección de intrusiones de red y Hola pila elástico. Monitor de red se proporciona con el paquete de saludo captura tooperform usa la detección de intrusiones de red. Captura de paquetes de saludo de Suricata procesos y las alertas de desencadenador se basan en paquetes que coincidan con su conjunto de reglas determinado de amenazas. Estas alertas se almacenan en un archivo de registro en la máquina local. Utilice Hola pila elástica, registros de hello generados por Suricata se pueden indizar y usan toocreate un panel de Kibana, le proporciona una representación visual de los registros de Hola y un vulnerabilidades de red significa tooquickly ganancia visión toopotential.  

![escenario sencillo de aplicación web][1]

Ambas herramientas de código abierto pueden configurarse en una máquina virtual de Azure, permitiéndole tooperform este análisis dentro de su propio entorno de red de Azure.

## <a name="steps"></a>Pasos

### <a name="install-suricata"></a>Instalación de Suricata

Para más información sobre todos los demás métodos de instalación, visite http://suricata.readthedocs.io/en/latest/install.html

1. En el terminal de línea de comandos de saludo de la máquina virtual ejecute Hola siguientes comandos:

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify la instalación, ejecute el comando de hello `suricata -h` lista completa de hello toosee de comandos.

### <a name="download-hello-emerging-threats-ruleset"></a>Descargar el conjunto de reglas de hello nuevas amenazas

En esta fase, no tenemos ninguna regla para Suricata toorun. Puede crear sus propias reglas si hay amenazas específicas de red tooyour le gustaría toodetect o también puede conjuntos de reglas de uso desarrolladas desde un número de proveedores, como nuevas amenazas o reglas VRT de Snort. Se utiliza el conjunto de reglas de hello libremente accesible nuevas amenazas aquí:

Descargar el conjunto de reglas de Hola y cópielos en el directorio de hello:

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Procesamiento de las capturas de paquetes con Suricata

captura de paquetes de tooprocess con Suricata, ejecute el siguiente comando de hello:

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck Hola resultante alertas, leer el archivo de Hola fast.log:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Configurar Hola pila elástica

Mientras que los registros de Hola que genera Suricata contienen información valiosa acerca de lo que ocurre en nuestra red, estos archivos de registro no son tooread más fácil de Hola y entenderán. Mediante la conexión Suricata con hello pila elástica, podemos crear un panel de Kibana lo que nos permite toosearch, gráfico, analizar y obtener la percepción de nuestros registros.

#### <a name="install-elasticsearch"></a>Instalación de Elasticsearch

1. Hola pila elástico desde la versión 5.0 y versiones posteriores requiere Java 8. Ejecute el comando de hello `java -version` toocheck su versión. Si no tiene java de instalación, consulte toodocumentation en [sitio Web de Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Descargue el paquete binario correcto de hello para el sistema:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Puede encontrar otros métodos de instalación en [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Instalación de Elasticsearch).

1. Compruebe que se está ejecutando con el comando Hola Elasticsearch:

    ```
    curl http://127.0.0.1:9200
    ```

    Debería ver un toothis similar de respuesta:

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

Para obtener más instrucciones sobre instalación búsqueda elástica, consulte toohello página [instalación](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Instalación de Logstash

1. tooinstall Logstash ejecute hello siguientes comandos:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. A continuación, necesitamos tooconfigure Logstash tooread de salida de hello del archivo eve.json. Cree un archivo logstash.conf mediante:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Agregar hello toohello contenido el archivo siguiente (asegúrese de que ese archivo de eve.json hello toohello de ruta de acceso sea correcto):

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. Asegúrese de que toogive Hola permisos correctos toohello eve.json el archivo para que Logstash puede introducir archivo hello.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash ejecutar comando hello:

    ```
    sudo /etc/init.d/logstash start
    ```

Para obtener más instrucciones acerca de cómo instalar Logstash, consulte toohello [documentación oficial](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-kibana"></a>Instalación de Kibana

1. Ejecute hello después comandos tooinstall Kibana:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. toorun Kibana use comandos de hello:

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. tooview web Kibana interfaz, vaya demasiado`http://localhost:5601`
1. En este escenario, el patrón de índice de hello utilizado para hello Suricata registra es "logstash-*"

1. Si desea Kibana panel de tooview Hola remotamente, cree una regla de NSG entrada permitir el acceso demasiado**puerto 5601**.

### <a name="create-a-kibana-dashboard"></a>Creación de un panel de Kibana

Para este artículo, proporcionamos un panel de ejemplo para que tooview tendencias y los detalles de las alertas.

1. Descargar archivo de panel de hello [aquí](https://aka.ms/networkwatchersuricatadashboard), archivo de visualización de hello [aquí](https://aka.ms/networkwatchersuricatavisualization)y el archivo de búsqueda de hello guarda [aquí](https://aka.ms/networkwatchersuricatasavedsearch).

1. En hello **administración** ficha de Kibana, navegue demasiado**objetos guardados** e importar los tres archivos. A continuación en hello **panel** ficha puede abrir y carga Hola panel de ejemplo.

También puede crear visualizaciones y paneles propios que se adapten a las métricas que le interesen. Puede leer más sobre la creación de visualizaciones de Kibana en la [documentación oficial](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana.

![panel de kibana][2]

### <a name="visualize-ids-alert-logs"></a>Visualización de registros de alertas de IDS

panel de ejemplo de Hola proporciona varias visualizaciones de registros de alertas de Hola Suricata:

1. Alertas por GeoIP: un mapa que muestra la distribución de Hola de alertas de su país de origen en función de la ubicación geográfica (determinado por IP)

    ![ip geográfica][3]

1. Top 10 alertas: un resumen de hello 10 más frecuentes desencadenada alertas y sus descripciones. Al hacer clic en una alerta individual filtra hacia abajo de la información del panel de hello toohello pertenecen toothat de alerta específica.

    ![imagen 4][4]

1. Número de alertas: Hola recuento total de alertas activadas por hello ruleset

    ![imagen 5][5]

1. 20 primeros origen/destino IP/puerto - que muestra los gráficos circulares Hola superior 20 direcciones IP y puertos que las alertas se han activado en. Puede filtrar hacia abajo en toosee de direcciones IP y puertos específico cuántas y qué tipo de alertas se desencadena.

    ![imagen 6][6]

1. Resumen de alertas: tabla que resume detalles específicos de cada alerta individual. Puede personalizar esta tabla tooshow otros parámetros de interés para cada alerta.

    ![imagen 7][7]

Para ver más documentación sobre la creación de visualizaciones y paneles personalizados, consulte la [documentación oficial del Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Conclusión

Al combinar las capturas de paquetes proporcionadas por Network Watcher con herramientas IDS de código abierto como Suricata, puede realizar la detección de intrusiones para una amplia variedad de amenazas. Estos paneles permiten tooquickly detectar tendencias y las anomalías dentro de la red, también adentrarse en hello causas raíz de toodiscover de datos de alertas, como agentes de usuario malintencionado o puertos vulnerables. Con estos datos extraídos, puede tomar decisiones informadas acerca de cómo tooreact tooand proteger su red de los intentos de intrusión perjudicial y crear reglas tooprevent futuras intrusiones tooyour red.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de la captura de paquetes de tootrigger alertas en función de si visita [usar paquetes captura toodo automático supervisión de red con funciones de Azure](network-watcher-alert-triggered-packet-capture.md)

Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
