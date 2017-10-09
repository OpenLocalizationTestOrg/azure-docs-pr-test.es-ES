Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada parámetros que contiene todos los valores de parámetro de Hola.
Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que siempre permanecerá Hola igual. Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan. 

Al definir parámetros, usar hello **allowedValues** toospecify campo los valores de un usuario puede proporcionar durante la implementación. Hola de uso **defaultValue** tooassign campo valor toohello parámetro, si se proporciona ningún valor durante la implementación.

Vamos a describir cada parámetro de plantilla de Hola.

### <a name="sitename"></a>siteName
nombre de Hola de aplicación web de hello que desea toocreate.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
nombre de Hola de servicio de aplicaciones de hello planear toouse para hospedar la aplicación web de hello.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>sku
Hola tarifa de hello plan de hospedaje.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

plantilla de Hello define los valores de hello permitidas para este parámetro y asigna un valor predeterminado (S1) si no se especifica ningún valor.

### <a name="workersize"></a>workerSize
tamaño de la instancia de Hola de hello plan (pequeño, mediano o grande) de hospedaje.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

Hola plantilla define los valores de hello permitidas para este parámetro (0, 1 o 2) y asigna un valor predeterminado (0) si no se especifica ningún valor. valores de Hello corresponden toosmall, mediana y grande.

