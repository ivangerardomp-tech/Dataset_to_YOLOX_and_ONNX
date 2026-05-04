# Dataset to YOLOX and ONNX

Repositorio público con notebooks de Google Colab para:

1. entrenar un modelo YOLOX desde un dataset en formato COCO,
2. exportar checkpoints `.pth` a ONNX,
3. empaquetar los nombres de clase dentro del metadato `names` del modelo ONNX,
4. descargar un ONNX final listo para integrar en aplicaciones web o pipelines de inferencia.

## Notebooks disponibles

### 1. Entrenar desde dataset ZIP COCO y exportar a ONNX
Abre en Colab:

[01_entrenar_y_exportar_yolox_a_onnx.ipynb](https://colab.research.google.com/github/ivangerardomp-tech/Dataset_to_YOLOX_and_ONNX/blob/main/01_entrenar_y_exportar_yolox_a_onnx.ipynb)

Este notebook:

- instala YOLOX y dependencias,
- recibe un dataset `.zip` en formato COCO,
- reorganiza el dataset dentro de Colab,
- entrena el modelo,
- exporta el mejor checkpoint a ONNX,
- inserta las clases en el metadato `names`,
- descarga el ONNX final.

### 2. Exportar un `.pth` ya entrenado a ONNX con clases manuales
Abre en Colab:

[02_exportar_yolox_pth_a_onnx_con_clases.ipynb](https://colab.research.google.com/github/ivangerardomp-tech/Dataset_to_YOLOX_and_ONNX/blob/main/02_exportar_yolox_pth_a_onnx_con_clases.ipynb)

Este notebook:

- no entrena,
- recibe un checkpoint `.pth` ya entrenado,
- permite ingresar manualmente la lista de clases,
- exporta el modelo a ONNX,
- empaqueta las clases en el metadato `names`,
- descarga el ONNX final.

### 3. Entrenar desde Roboflow y exportar a ONNX
Abre en Colab:

[03_entrenar_y_exportar_yolox_desde_roboflow_a_onnx.ipynb](https://colab.research.google.com/github/ivangerardomp-tech/Dataset_to_YOLOX_and_ONNX/blob/main/03_entrenar_y_exportar_yolox_desde_roboflow_a_onnx.ipynb)

Este notebook:

- instala YOLOX y dependencias,
- descarga el dataset desde Roboflow en formato COCO,
- entrena el modelo,
- exporta a ONNX,
- empaqueta las clases en el metadato `names`,
- descarga el ONNX final.

## Requisitos generales

- Cuenta de Google para usar Colab.
- GPU activa en Colab para notebooks de entrenamiento.
- Dataset en formato COCO si vas a entrenar.
- Checkpoint `.pth` si solo vas a exportar.
- Cuenta y API Key de Roboflow si vas a usar el notebook de Roboflow.

## Configuracion recomendada

- Los notebooks de entrenamiento usan `MAX_EPOCH = 50` por defecto.
- Los notebooks que exponen `INPUT_WIDTH` e `INPUT_HEIGHT` permiten entrenar y exportar modelos rectangulares.
- `INPUT_WIDTH` e `INPUT_HEIGHT` deben ser multiplos de 32 para YOLOX.
- Recomendaciones de tamano maximo:
  - `640x640` si el dataset es cuadrado
  - `1024x576` si la relacion de aspecto es 16:9 horizontal
  - `576x1024` si la relacion de aspecto es 16:9 vertical
- En el notebook de Roboflow debes pegar la URL publicada del dataset en:
  - `ROBOFLOW_DATASET_URL = "PEGA_AQUI_TU_DATASET_URL"`

## Formato de salida

El resultado final es un archivo `.onnx` con:

- el modelo exportado,
- decodificación lista para el flujo previsto en estos notebooks,
- metadato `names` con las clases del modelo.

Esto facilita integrar el modelo en aplicaciones que necesiten leer automáticamente las clases desde el propio ONNX.

## Estructura esperada del dataset

### Opción ZIP COCO
El notebook 1 fue preparado para una estructura similar a:

```text
dataset_.coco.zip
|-- test/
|   |-- _annotations.coco.json
|   |-- img1.jpg
|   `-- img2.jpg
|-- train/
|   |-- _annotations.coco.json
|   |-- img1.jpg
|   `-- img2.jpg
`-- valid/
    |-- _annotations.coco.json
    |-- img3.jpg
    `-- img4.jpg
```
