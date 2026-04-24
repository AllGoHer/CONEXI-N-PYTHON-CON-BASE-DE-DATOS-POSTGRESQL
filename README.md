# CONEXI-N-PYTHON-CON-BASE-DE-DATOS-POSTGRESQL ![image](https://github.com/user-attachments/assets/d947f562-da23-4e39-8f65-b695fb8e4816) ![image](https://github.com/user-attachments/assets/54ad4047-3868-43a5-937f-d899808fd9ec)
______________________________________________________________________________________________________________________________________________________________________________________________________________________________

1.	Primero creamos una base de datos en pgAdmin de PostgreSQL, haciendo click derecho en Databases.
   
   ![iamge](https://github.com/user-attachments/assets/7503a2db-5c1b-430d-bd08-5ab93ec09a4d)

   

   ![image](https://github.com/user-attachments/assets/02849009-b3d2-49f1-9dee-84ab5f4390c5)

2.	Luego hacemos click derecho en Schemas y seleccionamos Query tool para abrir el editor SQL.

    ![image](https://github.com/user-attachments/assets/f312d4b6-f18b-44d9-a191-44135a7d3a25)

3.	Creamos una base de datos llamado usuarios

   ![image](https://github.com/user-attachments/assets/75d9fb2f-4cbb-4173-874b-362f73fa659e)

   Verificamos la creación de la tabla escribiendo el siguiente comando:
 
   Select * from usuarios;

   Y podremos ver en la parte inferior del editor de código los encabezados de la tabla

   ![image](https://github.com/user-attachments/assets/0dd4c222-4e1b-458d-8b07-3c82f7cdec7a)

4.	Ahora que tenemos configurado la base de datos, nos vamos a nuestro editor de código (VSCode) de python y escribimos el código para conectar con la base de datos de PostgreSQL y verifica en la terminal que diga ¡Conexión exitosa!
   
codigo:
       
       import psycopg2

       try:
    
           conexion=psycopg2.connect(database='Base_Prueba', user='postgres', password='postgres')
    
           cursor01=conexion.cursor()
    
           cursor01.execute('select version()')
    
           version=cursor01.fetchone()

           # Imprimimos la versión si todo sale bien
    
           print("¡Conexión exitosa!")
    
           print(version)
    
           # CERRAMOS TODO AQUÍ DENTRO
    
           cursor01.close()
    
           conexion.close()
    
           print("Conexión cerrada correctamente.")
    
       except Exception as err:

           # Si algo falla, imprimimos el error y NO intentamos cerrar nada
    
           print("Error al conectar a la base:", err)


 ![image](https://github.com/user-attachments/assets/e5261e40-6c17-4c5d-87a8-4563274f994a)

Ojo: en caso de que la importación de la librería psycopg2 no cargue, intenta instalarlo con el siguiente código en la terminal.

   código:
   
           py -m pip install psycopg2-binary      

5.	Ahora proseguimos a insertar registros, lo cual modificaremos un poco el código para insertar los datos correctamente y mejorar el flujo a la base de datos.

código:

       import psycopg2

     try:
    
         conexion=psycopg2.connect(database='Base_Prueba', user='postgres', password='postgres')
    
         cursor01=conexion.cursor()
    
         cursor01.execute('select version()')
    
         version=cursor01.fetchone()

             # Imprimimos la versión si todo sale bien
        
         print("¡Conexión exitosa!")
    
         print(version)

         # Aqui insertamos los datos para la tabla
    
         cursor01.execute("insert into usuarios values(1001, 'Axel','admi2')")
    
         conexion.commit() # confirma los cambios en la base de datos.
    
         print('Datos insertados correctamente en la tabla.')

     except Exception as err:

         # Si algo falla (ej. la tabla no existe), entras aquí
    
         print('Ocurrió un error:', err)

     finally:

         # EL BLOQUE 'finally' SIRVE PARA LIMPIEZA: 
    
         # Se ejecuta SIEMPRE, haya error o no.
    
         # Pero debemos verificar que 'conexion' exista antes de cerrarla.
    
         try:
        
             cursor01.close()
        
             conexion.close()
        
             print("Conexión cerrada correctamente.")
        
         except:
    
             pass # Si nunca se abrió, no hay nada que cerrar, así que ignoramos el error

6.	Finalmente verificamos en la terminal que el código haya corrido exitosamente y que haya enlazado correctamente con la base de datos PostgreSQL. 

![image](https://github.com/user-attachments/assets/a6092abf-8422-4552-8b64-b7251da2adad)

![image](https://github.com/user-attachments/assets/8c9ad69b-fd8c-421b-a5cd-9744c2b16c96)




