Normalmente una aplicación que hace uso de AI localmente sigue los siguientes pasos:

1. **Carga del modelo**: Se carga el modelo `.tflite` en memoria, el cual contiene el grafo de ejecución
2. **Transformación de la data**: Se transforma la data input al formato y dimensiones esperados. Normalmente la data "cruda"(Raw) no calza con lo esperado por el modelo. Por ejemplo, podrías necesitar redimensionar una imágen, o cambiar el formato.
3. **Correr la inferencia**: Se ejecuta el modelo para hacer predicciones. Este paso involucra ejecutar el API de LiteRT / TensorFlow Lite para ejecutar el modelo. Acá se puede construir el intérprete, y definir y asignar espacio para tensores.
4. **Interpretar el output**: Interpretar el output de manera útil para tu aplicación. Por ejemplo, un modelo podría retornar una lista de probabilidades, depende de ti mapear las probabilidades a categorias y formatear el output.

En el contexto de una app Android.

![[Pasted image 20251103033128.png]]