# Discord Image Classifier Bot

Bot de Discord que utiliza un modelo de *TensorFlow/Keras* para clasificar imágenes enviadas por los usuarios.
El bot analiza la imagen subida en un mensaje y responde con la predicción del modelo.

---

## Características

* Clasificación automática de imágenes (limitado a 3 clasificaciones)
* Integración con un modelo .h5 de Keras
* Lectura de etiquetas desde labels.txt
* Comando simple para analizar imágenes
* Compatible con bots creados con *discord.py*

---

## Requisitos

Antes de ejecutar el proyecto, instala las siguientes dependencias:

* Python 3.8+
* discord.py
* TensorFlow
* NumPy

Instalación:

bash
pip install discord.py tensorflow numpy


---

## Estructura del proyecto


project/
│
├── bot.py
├── model.py
├── keras_model.h5
├── labels.txt
└── README.md


### Descripción de archivos

* *bot.py* → código principal del bot de Discord
* *model.py* → función get_class() que carga el modelo y realiza la predicción
* *keras_model.h5* → modelo entrenado
* *labels.txt* → etiquetas de clasificación

---

## Uso del bot

El bot incluye el comando:
$check

Tambien contiene los comandos:
$duck (entrega una imagen de un pato)
$hello (dice hola al usuario (en ingles))
$heh (repite la palabra "he" el numero de veces especificado (ejemplo de uso: $heh 4))

### Cómo usarlo

1. Escribe el comando en un canal donde esté el bot.
2. Adjunta una imagen en el mismo mensaje.
3. El bot analizará la imagen y responderá con la clasificación.

Ejemplo:


$check


(con una imagen de un gato adjunta)

Respuesta del bot:


Gato (92.4%)


Si no se adjunta ninguna imagen:


Olvidaste subir la imagen :(


---

## Código del comando

python
@bot.command()
async def check(ctx):
    if ctx.message.attachments:
        for attachment in ctx.message.attachments:
            file_name = attachment.filename
            file_url = attachment.url
            await attachment.save(f"./{attachment.filename}")
            await ctx.send(get_class(model_path="./keras_model.h5", labels_path="labels.txt", image_path=f"./{attachment.filename}"))
    else:
        await ctx.send("You forgot to upload the image :(")


---

## Posibles mejoras

* Mostrar el porcentaje de confianza de la predicción
* Eliminar automáticamente las imágenes después de analizarlas
* Soporte para múltiples modelos
* Interfaz web usando Flask

---

## Licencia

Este proyecto es de uso educativo y puede ser modificado libremente.
