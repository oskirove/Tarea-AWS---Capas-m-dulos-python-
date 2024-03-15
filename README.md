# Envío de Mensajes a Discord con AWS Lambda (Python)

## 1. Actualizar el Código

Antes de comenzar, actualizaremos el código para que funcione como una función de Lambda. Eliminaremos las partes relacionadas con el webhook de Discord y reemplazaremos la función `lambda_handler` para que envíe un mensaje simple. 

Aquí se muestra el código actualizado:

```python
import json

def lambda_handler(event, context):
    message = "Hello from Discord Lambda!"
    print(message)
    return {
        'statusCode': 200,
        'body': json.dumps(message)
    }
```

## 2. Instalar Dependencias y Empaquetar el Código

Para instalar las dependencias necesarias y empaquetar el código para su uso en AWS Lambda, seguiremos estos pasos:

- **Instalaremos la biblioteca `discord-webhook` utilizando pip:**

  ```bash
  pip install discord-webhook
  ```

- **Crear un archivo `requirements.txt` con el nombre de todas las dependencias:**

  Ejecutamos el siguiente comando para crear el archivo `requirements.txt`:

  ```bash
  echo "discord-webhook" > requirements.txt
  ```

- **Empaquetar el código y las dependencias en un archivo zip:**

  Nos aseguramos de estar en el directorio que contiene nuestro código y el archivo `requirements.txt`, luego ejecutamos el siguiente comando:

  ```bash
  zip -r lambda_function.zip ./*
  ```

## 3. Crear y Configurar la Función Lambda en AWS

- **Vamos a la consola de AWS Lambda y creamos una nueva función Lambda.**

- **Seleccionamos Python como el lenguaje de programación y elegimos la opción para cargar un archivo zip.**

- **Cargamos el archivo `lambda_function.zip` que acabamos de crear.**

## 4. Configurar Triggers y Permisos (Opcional)

Si es necesario, configuramos los triggers y los permisos de la función Lambda según nuestras necesidades. Por ejemplo, podemos configurar un trigger para que la función se ejecute en respuesta a un evento específico, como un evento de Amazon S3.

## 5. Probar la Función Lambda

Una vez que la función Lambda esté creada, podemos probarla desde la consola de AWS Lambda. Después de ejecutarla, podemos verificar si el mensaje "Hello from Discord Lambda!" se imprime en los logs de CloudWatch.

## Ejecución de la Aplicación en Python para Actualizar un Mensaje

Si deseamos ejecutar la aplicación en nuestro entorno local para actualizar un mensaje, seguimos estos pasos adicionales:

- **Creamos un Virtual Environment (Entorno Virtual):**

  - Utilizamos el siguiente comando para crear un nuevo entorno virtual:

    ```bash
    python3 -m venv venv
    ```

  - Activamos el entorno virtual:

      ```bash
      source venv/bin/activate
      ```

- **Configuramos la Capa de Funciones en AWS:**

  - Creamos un paquete zip que contenga las bibliotecas externas necesarias y lo subimos a AWS Layers.
  
  - Asociamos la capa creada con la función Lambda que ejecutará la aplicación.

>[!NOTE]
>Siguiendo estos pasos, habremos configurado y ejecutado con éxito nuestra función Lambda en AWS para enviar un mensaje a Discord, y también estaremos listos para ejecutar la aplicación en nuestro entorno local para actualizar mensajes.
