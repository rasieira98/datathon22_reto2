![image](https://user-images.githubusercontent.com/116558787/197547402-7aea89ce-1cf8-4156-830a-a0a822622aa3.png)
# RETO 2:Cancelación de Ruido
## GRUPO_70: Ramón Sieira Martínez (SDG Group) José Divasón (Universidad de La Rioja) Francisco Javier Martínez de Pisón (Universidad de La Rioja)
 - El problema consiste en la reducción del ruido sin contar con
   muestras ‘limpias’, es decir, entrenar exclusivamente con fragmentos
   de ruido. En este reciente trabajo utilizan un decoder-encoder U-NET
   de 20 capas (DCUnet-20) para la eliminación del ruido en grabaciones
   de lenguaje hablado SIN UTILIZAR MUESTRAS LIMPIAS. 
 - Nuestra inquietud surgió de si este modelo podía reentrenarse con sonido marino en vez
   de otros tipos de ruido. La idea es muy interesante pues utiliza un
   Encoder-Decoder que es capaz de ‘condensar’ la descripción de los
   información en el domino complejo obtenido con la transformada
   discreta de Fourier. La idea es, que el modelo sea capaz de
   “reconstruir” desde el dominio complejo la “estructura” del ruido
   para poder luego volver a descomponerlo para restárselo al
   espectrograma y con la transformada inversa de Fourier, obtener la
   señal filtrada.
   ![image](https://user-images.githubusercontent.com/116558787/197547069-e97d1bc0-03df-4e2a-9650-4cd20fb7addc.png)
 - El problema consistió en entrenar el modelo con el  audio suministrado PERO sin eventos. Una vez entrenado el modelo, se
   puede usar para limpiar audios marinos. El entrenamiento del modelo
   se realizó con muestras de ruido donde NO EXISTIAN EVENTOS. Al no
   disponer de muestras limpias, y no tener tiempo para limpiarlas, se
   fueron comprobando los modelos obtenidos de cada epoch mediante
   escucha de los audios obtenidos. El modelo seleccionado fue el del
   epoch que mejor resultados dio. Una vez se dispone del modelo, es
   fácil y rápido limpiar los audios. Sin embargo, para mejorar la
   calidad del audio, se realiza un filtrado fino con métodos clásicos.
   Este filtrado no es demasiado agresivo y tiene como objetivo
   “suavizar” los resultados del modelo DCUnet-20.
   ![image](https://user-images.githubusercontent.com/116558787/197547170-19c4f194-d0b5-4efa-b098-46eb7d045c22.png)

  - Aqui hay un modelo que se puede cargar en la parte de inferencia(El 4 es el usado para el submission):  https://drive.google.com/drive/folders/1-J1EYMPdLv4sujIB0OEZTGivvrxzCvwx?usp=sharing
  - Este seria un ejemplo de los datos SIN ruido: https://drive.google.com/drive/folders/18xWqETAnWEEkKjZu-mZ94QOxIE6ZEBqj?usp=sharing
  - El repo en el que nos hemos basado: https://github.com/madhavmk/Noise2Noise-audio_denoising_without_clean_training_data
