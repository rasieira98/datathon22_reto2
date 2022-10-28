![image](https://user-images.githubusercontent.com/116558787/197547402-7aea89ce-1cf8-4156-830a-a0a822622aa3.png)
# RETO 2: Cancelación de Ruido
## GRUPO_70: Ramón Sieira Martínez (SDG Group), Francisco Javier Martínez de Pisón (Universidad de La Rioja) y Jose Divasón (Universidad de La Rioja)
 - El reto consiste en la reducción del ruido de fragmentos de audios marinos, 
   con la complejidad añadida de no contar con muestras limpias, es decir,
   se dispone solo de fragmentos que contienen ruido para el entrenamiento. 
  - En un reciente trabajo (ver [1]) se utiliza un decoder-encoder U-NET
   de 20 capas (DCUnet-20) para la eliminación del ruido en grabaciones
   de lenguaje hablado SIN UTILIZAR MUESTRAS LIMPIAS. 
   La idea es muy interesante pues utiliza un
   Encoder-Decoder que es capaz de ‘condensar’ la descripción de los
   información en el domino complejo obtenido con la transformada
   discreta de Fourier. La idea es, que el modelo sea capaz de
   “reconstruir” desde el dominio complejo la “estructura” del ruido
   para poder luego volver a descomponerlo para restárselo al
   espectrograma y con la transformada inversa de Fourier, obtener la
   señal filtrada.
   ![image](https://user-images.githubusercontent.com/116558787/197547069-e97d1bc0-03df-4e2a-9650-4cd20fb7addc.png)
 - Nuestra propuesta consiste en reentrenar dicho modelo con los fragmentos de sonido marino con ruido suministrados,
   pero los recortamos para eliminar los eventos, de manera que la red neuronal no reciba como entrada sonido de cetáceos.
   Una vez entrenado el modelo, se
   puede usar para limpiar audios marinos. Al no
   disponer de muestras limpias, y no tener tiempo para limpiarlas, se
   fueron comprobando los modelos obtenidos de cada epoch mediante la
   escucha de los audios obtenidos. El modelo seleccionado fue el del
   epoch que mejor resultados dio. Una vez se dispone del modelo, es
   fácil y rápido limpiar los audios. Sin embargo, para mejorar la
   calidad del audio, se realiza un filtrado fino con métodos clásicos.
   Este filtrado no es demasiado agresivo y tiene como objetivo
   “suavizar” los resultados del modelo DCUnet-20.
   ![image](https://user-images.githubusercontent.com/116558787/197547170-19c4f194-d0b5-4efa-b098-46eb7d045c22.png)

  ### Ejemplos
  
  - Aquí hay un modelo que se puede cargar en la parte de inferencia (el 4 es el usado para el envío):  https://drive.google.com/drive/folders/1-J1EYMPdLv4sujIB0OEZTGivvrxzCvwx?usp=sharing
  - Este sería un ejemplo de los datos SIN ruido: https://drive.google.com/drive/folders/18xWqETAnWEEkKjZu-mZ94QOxIE6ZEBqj?usp=sharing
  
  ### Referencias
  
  [1] Kashyap, M.M., Tambwekar, A., Manohara, K., Natarajan, S. (2021) Speech Denoising Without Clean Training Data: A Noise2Noise Approach. Proc. Interspeech 2021, 2716-2720, doi: 10.21437/Interspeech.2021-1130
