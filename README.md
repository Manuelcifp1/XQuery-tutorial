# XQUERY

<br>
XQuery es un lenguaje para realizar consultas y procesar datos en XML.
Se podría decir que sería el SQL para datos en XML.

Para realizar una consulta en XQuery hay que apoyarse en XPath. 
Hay que referirse al XML en el que queremos hacer la consulta mediante la siguiente función:

    fn:doc(“nombre_del_xml”)

y después de ella, añadimos la consulta como hacemos en XPath:

    fn:doc(“nombre_del_xml”)/libro/titulo

Al igual que en XPath, así obtenemos el título del libro o los títulos de todos los libros si hay más en el XML. 

Al respecto de las sentencias FLWOR ( For Let Where Order Return), con ellas podemos unir variables de conjuntos de nodos.

Su estructura sería la siguiente:

* FOR: enlaza una o más variables a expresiones XPath.
* LET: enlaza una variable al resultado de una expresión y enlazando también con  el/los  resultado de la cláusula FOR.
* WHERE: establece las condiciones para los resultados anteriores.
* ORDER BY: sirve para ordenar los resultados.
* RETURN: nos muestra la estructura de los resultados.

Podemos integrar HTML en XQuery, para que nos de resultados que se puedan abrir en un navegador. Se hace de una manera similar a la que utilizamos en XSLT, situando expresiones de XQuery entre etiquetas de HTML.

Aquí podemos ver un ejemplo de ello:

Tenemos este XML, books.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<books>
   
   <book category="JAVA">
      <title lang="en">Learn Java in 24 Hours</title>
      <author>Robert</author>
      <year>2005</year>
      <price>30.00</price>
   </book>
   
   <book category="DOTNET">
      <title lang="en">Learn .Net in 24 hours</title>
      <author>Peter</author>
      <year>2011</year>
      <price>70.50</price>
   </book>
   
   <book category="XML">
      <title lang="en">Learn XQuery in 24 hours</title>
      <author>Robert</author>
      <author>Peter</author> 
      <year>2013</year>
      <price>50.00</price>
   </book>
   
   <book category="XML">
      <title lang="en">Learn XPath in 24 hours</title>
      <author>Jay Ban</author>
      <year>2010</year>
      <price>16.50</price>
   </book>
   
</books>
```

<br>

Le aplicamos esta expresión XQuery con etiquetas HTML para convertir el resultado en una tabla:

```html
let $books := (doc("books.xml")/books/book)
return <table><tr><th>Title</th><th>Price</th></tr>
{
   for $x in $books   
   order by $x/price
   return <tr><td>{data($x/title)}</td><td>{data($x/price)}</td></tr>
}
</table>
</results
```

<br>

Y obtenemos el siguiente resultado:
```html
<table>
   <tr>
      <th>Title</th>
      <th>Price</th>
   </tr>
   <tr>
      <td>Learn XPath in 24 hours</td>
      <td>16.50</td>
   </tr>   
   <tr>
      <td>Learn Java in 24 Hours</td>
      <td>30.00</td>
   </tr>
   <tr>
      <td>Learn XQuery in 24 hours</td>
      <td>50.00</td>
   </tr>   
   <tr>
      <td>Learn .Net in 24 hours</td>
      <td>70.50</td>
   </tr>
</table>
```
<br>

Resumiendo, con XQuery tenemos otro lenguaje más para la consulta de documentos en XML. Algo más complejo que XPath o XSLT ya que utiliza variables al igual que PHP.


