Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada parámetros que contiene todos los valores de parámetro de Hola.
Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que siempre permanecerá Hola igual. Cada valor del parámetro se utiliza en Hola Hola de toodefine plantilla implementación recursos. 

Al definir parámetros, usar hello **allowedValues** toospecify campo los valores de un usuario puede proporcionar durante la implementación. Hola de uso **defaultValue** tooassign campo valor toohello parámetro, si se proporciona ningún valor durante la implementación.

Vamos a describir cada parámetro de plantilla de Hola.

### <a name="logicappname"></a>logicAppName
nombre de Hola de toocreate de aplicación lógica de Hola.

    "logicAppName": {
        "type": "string"
    }