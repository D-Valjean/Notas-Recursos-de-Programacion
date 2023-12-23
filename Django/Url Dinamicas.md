Para crear de forma mas eficiente las url en consecutivo, debemos crear un variable global donde vamos almacenar las urls que vayamos creando, lo hacemos en la raiz del proyecto
![[Pasted image 20231222154622.png]]
Dentro de ella declaramos una lista vacia en ella 
![[Pasted image 20231222155219.png]]

Luego en cada app en nuestro proyecto, en las urls.py importamos esta variable:
	from mycore.global_url.py import global_urls
Al final de declarar las urls en *urlpatterns* , las agragamos a nuestra variable
![[Pasted image 20231222162443.png]]
# UPDATE
![[Pasted image 20231222163642.png]] 
Modo Automatico

De esta forma, tenemos una lista de todas nuestras dirrecciones, la cual podemos llamar en nuestra vistas por la funcion get_context_data
![[Pasted image 20231222132309.png]]
