## <a name="traffic-manager-profile"></a>Perfil del Administrador de tráfico
El Administrador de tráfico y su recurso de extremo secundario permiten tooendpoints de enrutamiento de DNS en Azure y fuera de Azure. Esta distribución de tráfico se rige por los métodos de directivas de enrutamiento. Traffic manager también permite supervisa toobe de estado de punto de conexión y tráfico desviado adecuadamente basadas en el estado de saludo de un punto de conexión. 

| Propiedad | Descripción |
| --- | --- |
| **trafficRoutingMethod** |los valores posibles son *Performance*, *Weighted* y *Priority* |
| **dnsConfig** |FQDN para el perfil de Hola |
| **Protocolo** |protocolo de supervisión, los valores posibles son *HTTP* y *HTTPS* |
| **Puerto** |puerto de supervisión |
| **Ruta de acceso** |ruta de acceso de supervisión |
| **Extremos** |contenedor de recursos de punto de conexión |

### <a name="endpoint"></a>Extremo
Un extremo es un recurso secundario de un perfil de Administrador de tráfico. Representa un servicio o se distribuye el tráfico de usuario de web extremo toowhich basándose en la directiva de hello configurado en hello recursos de perfil de Traffic Manager. 

| Propiedad | Descripción |
| --- | --- |
| **Tipo** |Hola tipo de punto de conexión de hello, los valores posibles son *punto final de Azure*, *extremo externo*, y *extremo anidados* |
| **targetResourceId** |dirección IP pública de servicio o punto de conexión web. Puede tratarse de un extremo de Azure o uno externo. |
| **Peso** |ponderación del punto de conexión usada en la administración del tráfico. |
| **Prioridad** |prioridad de punto de conexión de hello, toodefine usa una acción de conmutación por error |

Ejemplo de Administrador de tráfico en formato Json: 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>Recursos adicionales
Para más información, lea la [documentación de API de REST para el Administrador de tráfico](https://msdn.microsoft.com/library/azure/mt163664.aspx) .

