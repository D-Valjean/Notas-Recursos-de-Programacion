
[Libreria xhtml2pdf](https://xhtml2pdf.readthedocs.io/en/latest/index.html)

Metodo para imprimir de forma simple en pdf, desventaja que no toma los estilos css ni bootstrap


# Funcion View:
	from .utils import render_to_pdf
	class List_huespedes_PDF(View):
	
	  
	
	    def get(self, request, *args, **kwargs):
	
	        huespedes = Huesped.objects.all()
	
	        habitacion = Habitacion.objects.all()
	
	        ocupacion = habitacion.filter(habitacion)
	
	        data = {
	
	            'huespedes': huespedes,
	
	            'habitacion': habitacion
	
	        }
	
	        pdf = render_to_pdf('Huesped/list_huesped.html', data)
	
	        return HttpResponse(pdf, content_type='application/pdf')

# Utils.py 
	
	from django.template.loader import get_template
	
	from io import BytesIO
	
	from django.http import HttpResponse
	
	from xhtml2pdf import pisa
	
	  
	  
	
	def render_to_pdf(template_src, context_dict={}):
	
	    template = get_template(template_src)
	
	    html = template.render(context_dict)
	
	    result = BytesIO()
	
	    pdf = pisa.pisaDocument(BytesIO(html.encode("ISO-8859-1")), result)
	
	    if not pdf.err:
	
	        return HttpResponse(result.getvalue(), content_type='application/pdf')
	
	    return None