Colección de medidas personalizadas. Utilice este tooreport de colección con el nombre de medida asociado con el elemento de telemetría de Hola. Casos de uso típicos:
- tamaño de Hola de carga de telemetría de dependencia
- número de Hola de elementos de la cola procesados por solicitud de telemetría
- tiempo que el cliente tardó toocomplete Hola paso en la finalización de paso del Asistente para la telemetría de eventos.

Puede consultar las [medidas personalizadas](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) en el análisis de aplicaciones:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Medidas personalizadas están asociadas al elemento de telemetría de Hola que pertenecen. Únicamente son toosampling de asunto con el elemento de telemetría de Hola que contiene esas mediciones. una medida que tiene un valor independiente de otros tipos de telemetría, use tootrack [telemetría métrica](../articles/application-insights/app-insights-api-custom-events-metrics.md).

Longitud máxima de la clave: 150
