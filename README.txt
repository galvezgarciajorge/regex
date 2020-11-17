


// Al introducirle la funcion /R/ a la instruccion $regex tiene que encontrar las filas que empizan por "C" en el apartado de "Ciudades".


> db.regex.find( { ciudad: { $regex: /C/ } } )
{ "_id" : ObjectId("5fa990c8407e64eed96b0805"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Seteneil de las bodegas", "habitantes" : "2.769", "gentilicio" : "setenileño", "Monumento_hitorico" : "Fortaleza Nazari" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0807"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Olvera", "habitantes" : "8.124", "gentilicio" : "olvereño", "Monumento_hitorico" : "Castillo de Olvera" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0808"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Tarifa", "habitantes" : "18.169", "gentilicio" : "tarifeño", 
"Monumento_hitorico" : "Ruinas romanas de Baelo Claudia" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0809"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Zahara de la sierra", "habitantes" : "1.400", "gentilicio" : 
"zahareño", "Monumento_hitorico" : "Iglesia mayor" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080e"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Conil de la frontera", "habitantes" : "22.427", "gentilicio" 
: "cooleño", "Monumento_hitorico" : "Iglesia de Santa Catalina" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080f"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Vejer de la frontera", "habitantes" : "12.739", "gentilicio" 
: "vejeriego", "Monumento_hitorico" : "Torre del Mayorazgo" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0811"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Priego de Cordoba", "habitantes" : "22.285", "gentilicio" : "prieguense", "Monumento_hitorico" : "Iglesia de la Aurora" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0812"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Iznajar", "habitantes" : "4.343", "gentilicio" : "iznajeño", "Monumento_hitorico" : "Castillo de Iznajar" }


// Introduciendo el $gt y $regex, consigo filtrar mi consulta habitantes de mas de 10.000 ($gt) y que empienzen su nombre por T ($regex: /T/)

> db.regex.find( { $and: [ { "habitantes": { $gt: "10.000" } }, { "pueblo": { $regex: /T/ } } ] } ) 
{ "_id" : ObjectId("5fa990c8407e64eed96b0808"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Tarifa", "habitantes" : "18.169", "gentilicio" : "tarifeño", 
"Monumento_hitorico" : "Ruinas romanas de Baelo Claudia" }


// En este caso es puesto un filtro de cantidad ($in:) basandonos en los habitantes.

> db.regex.find( { "habitantes": { $in: [ "19.510", "52.617" ] } } )
{ "_id" : ObjectId("5fa990c8407e64eed96b080a"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Utrera", "habitantes" : "52.617", "gentilicio" : "utrerano", "Monumento_hitorico" : "Iglesia Santa Maria de la Mesa" }


// Esta consulta es una consulta directa a un campo, en mi caso es la ciudades de Jaen 

db.regex.find( { "ciudad": { $eq: "Jaen" } } )  
{ "_id" : ObjectId("5fa990c8407e64eed96b0815"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Andujar", "habitantes" : "37.113", "gentilicio" : "andujareño", "Monumento_hitorico" : "Basilica de Nuestra Señora de las Cabeza" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0816"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Baeza", "habitantes" : "15.902", "gentilicio" : "baezano", "Monumento_hitorico" : "La plaza de Santa Maria" }

//Esta consulta es una comparativa entre habitantes de pueblos que tengan menos de 100.000 y 50.000

db.regex.find( { $or: [ { "habitantes": { $lt: "100.000" } }, { "habitantes":{ $gt: "50.000" }} ] } )
{ "_id" : ObjectId("5fa990c8407e64eed96b0807"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Olvera", "habitantes" : "8.124", "gentilicio" : "olvereño", "Monumento_hitorico" : "Castillo de Olvera" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0809"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Zahara de la sierra", "habitantes" : "1.400", "gentilicio" : 
"zahareño", "Monumento_hitorico" : "Iglesia mayor" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080a"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Utrera", "habitantes" : "52.617", "gentilicio" : "utrerano", "Monumento_hitorico" : "Iglesia Santa Maria de la Mesa" }

//Esta consulta es para descartar lo que se encuentre dentro de los corchete []

db.regex.find( { "habitantes": { $nin: [100.000, 55.000 ] } } )   
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e6998a"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Carmona", "habitantes" : "28.620", "gentilicio" : "carmonense", "Monumento_hitorico" : "Necropolis romana" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e6998b"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Conil de la frontera", "habitantes" : "22.427", "gentilicio" 
: "cooleño", "Monumento_hitorico" : "Iglesia de Santa Catalina" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e6998c"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Vejer de la frontera", "habitantes" : "12.739", "gentilicio" 
: "vejeriego", "Monumento_hitorico" : "Torre del Mayorazgo" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e6998d"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Marbella", "habitantes" : "141.463", "gentilicio" : "marbelli", "Monumento_hitorico" : "Villa Romana" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e6998e"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Priego de Cordoba", "habitantes" : "22.285", "gentilicio" : "prieguense", "Monumento_hitorico" : "Iglesia de la Aurora" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e6998f"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Iznajar", "habitantes" : "4.343", "gentilicio" : "iznajeño", "Monumento_hitorico" : "Castillo de Iznajar" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e69990"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Montefrio", "habitantes" : "5.479", "gentilicio" : "montefrieño", "Monumento_hitorico" : "El pateon y viejo cementerio" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e69991"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Salobreña", "habitantes" : "12.396", "gentilicio" : "salobreño", "Monumento_hitorico" : "El castillo de Salobreña" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e69992"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Andujar", "habitantes" : "37.113", "gentilicio" : "andujareño", "Monumento_hitorico" : "Basilica de Nuestra Señora de las Cabeza" }
{ "_id" : ObjectId("5fa9a5fc2d1ea25d84e69993"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Baeza", "habitantes" : "15.902", "gentilicio" : "baezano", "Monumento_hitorico" : "La plaza de Santa Maria" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080b"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Los Palacios", "habitantes" : "38.246", "gentilicio" : "palaciegos", "Monumento_hitorico" : "Parroquia Mayor" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080c"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Moron de la Frontera", "habitantes" : "27.844", "gentilicio" : "moronero", "Monumento_hitorico" : "Castillo arabe" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080d"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Carmona", "habitantes" : "28.620", "gentilicio" : "carmonense", "Monumento_hitorico" : "Necropolis romana" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080e"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Conil de la frontera", "habitantes" : "22.427", "gentilicio" 
: "cooleño", "Monumento_hitorico" : "Iglesia de Santa Catalina" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080f"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Vejer de la frontera", "habitantes" : "12.739", "gentilicio" 
: "vejeriego", "Monumento_hitorico" : "Torre del Mayorazgo" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0810"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Marbella", "habitantes" : "141.463", "gentilicio" : "marbelli", "Monumento_hitorico" : "Villa Romana" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0811"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Priego de Cordoba", "habitantes" : "22.285", "gentilicio" : "prieguense", "Monumento_hitorico" : "Iglesia de la Aurora" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0812"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Iznajar", "habitantes" : "4.343", "gentilicio" : "iznajeño", "Monumento_hitorico" : "Castillo de Iznajar" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0813"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Montefrio", "habitantes" : "5.479", "gentilicio" : "montefrieño", "Monumento_hitorico" : "El pateon y viejo cementerio" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0814"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Salobreña", "habitantes" : "12.396", "gentilicio" : "salobreño", "Monumento_hitorico" : "El castillo de Salobreña" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0815"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Andujar", "habitantes" : "37.113", "gentilicio" : "andujareño", "Monumento_hitorico" : "Basilica de Nuestra Señora de las Cabeza" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0816"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Baeza", "habitantes" : "15.902", "gentilicio" : "baezano", "Monumento_hitorico" : "La plaza de Santa Maria" }
{ "_id" : ObjectId("5fa9a453308668f49486fd57"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Dos hermanas", "habitantes" : "130.000", "gentilicio" : "nazareno", "Monumento_hitorico" : "Alqueria del Pilar" }
{ "_id" : ObjectId("5fa9a453308668f49486fd58"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Seteneil de las bodegas", "habitantes" : "2.769", "gentilicio" : "setenileño", "Monumento_hitorico" : "Fortaleza Nazari" }
{ "_id" : ObjectId("5fa9a453308668f49486fd59"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Ronda", "habitantes" : "34.000", "gentilicio" : "rondeño", "Monumento_hitorico" : "Punte del Tajo" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5a"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Olvera", "habitantes" : "8.124", "gentilicio" : "olvereño", "Monumento_hitorico" : "Castillo de Olvera" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5b"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Tarifa", "habitantes" : "18.169", "gentilicio" : "tarifeño", 
"Monumento_hitorico" : "Ruinas romanas de Baelo Claudia" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5c"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Zahara de la sierra", "habitantes" : "1.400", "gentilicio" : 
"zahareño", "Monumento_hitorico" : "Iglesia mayor" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5d"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Utrera", "habitantes" : "52.617", "gentilicio" : "utrerano", "Monumento_hitorico" : "Iglesia Santa Maria de la Mesa" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5e"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Los Palacios", "habitantes" : "38.246", "gentilicio" : "palaciegos", "Monumento_hitorico" : "Parroquia Mayor" }


Busca en todas las ciudades que no sea Cadiz y que no tenga Iglesia en su Monumento_historico.

//db.regex.find( { $nor: [ { Nombre: "Cadiz" }, { Monumento_historico: { $regex: /Iglesia/ }} ]})
{ "_id" : ObjectId("5fa990c8407e64eed96b0804"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Dos hermanas", "habitantes" : "130.000", "gentilicio" : "nazareno", "Monumento_hitorico" : "Alqueria del Pilar" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0805"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Seteneil de las bodegas", "habitantes" : "2.769", "gentilicio" : "setenileño", "Monumento_hitorico" : "Fortaleza Nazari" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0806"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Ronda", "habitantes" : "34.000", "gentilicio" : "rondeño", "Monumento_hitorico" : "Punte del Tajo" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0807"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Olvera", "habitantes" : "8.124", "gentilicio" : "olvereño", "Monumento_hitorico" : "Castillo de Olvera" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0808"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Tarifa", "habitantes" : "18.169", "gentilicio" : "tarifeño", 
"Monumento_hitorico" : "Ruinas romanas de Baelo Claudia" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0809"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Zahara de la sierra", "habitantes" : "1.400", "gentilicio" : 
"zahareño", "Monumento_hitorico" : "Iglesia mayor" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080a"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Utrera", "habitantes" : "52.617", "gentilicio" : "utrerano", "Monumento_hitorico" : "Iglesia Santa Maria de la Mesa" }
Type "it" for more
> it
{ "_id" : ObjectId("5fa990c8407e64eed96b080b"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Los Palacios", "habitantes" : "38.246", "gentilicio" : "palaciegos", "Monumento_hitorico" : "Parroquia Mayor" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080c"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Moron de la Frontera", "habitantes" : "27.844", "gentilicio" : "moronero", "Monumento_hitorico" : "Castillo arabe" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080d"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Carmona", "habitantes" : "28.620", "gentilicio" : "carmonense", "Monumento_hitorico" : "Necropolis romana" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080e"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Conil de la frontera", "habitantes" : "22.427", "gentilicio" 
: "cooleño", "Monumento_hitorico" : "Iglesia de Santa Catalina" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080f"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Vejer de la frontera", "habitantes" : "12.739", "gentilicio" 
: "vejeriego", "Monumento_hitorico" : "Torre del Mayorazgo" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0810"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Marbella", "habitantes" : "141.463", "gentilicio" : "marbelli", "Monumento_hitorico" : "Villa Romana" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0811"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Priego de Cordoba", "habitantes" : "22.285", "gentilicio" : "prieguense", "Monumento_hitorico" : "Iglesia de la Aurora" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0812"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Iznajar", "habitantes" : "4.343", "gentilicio" : "iznajeño", "Monumento_hitorico" : "Castillo de Iznajar" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0813"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Montefrio", "habitantes" : "5.479", "gentilicio" : "montefrieño", "Monumento_hitorico" : "El pateon y viejo cementerio" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0814"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Salobreña", "habitantes" : "12.396", "gentilicio" : "salobreño", "Monumento_hitorico" : "El castillo de Salobreña" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0815"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Andujar", "habitantes" : "37.113", "gentilicio" : "andujareño", "Monumento_hitorico" : "Basilica de Nuestra Señora de las Cabeza" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0816"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Baeza", "habitantes" : "15.902", "gentilicio" : "baezano", "Monumento_hitorico" : "La plaza de Santa Maria" }
{ "_id" : ObjectId("5fa9a453308668f49486fd57"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Dos hermanas", "habitantes" : "130.000", "gentilicio" : "nazareno", "Monumento_hitorico" : "Alqueria del Pilar" }
{ "_id" : ObjectId("5fa9a453308668f49486fd58"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Seteneil de las bodegas", "habitantes" : "2.769", "gentilicio" : "setenileño", "Monumento_hitorico" : "Fortaleza Nazari" }
{ "_id" : ObjectId("5fa9a453308668f49486fd59"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Ronda", "habitantes" : "34.000", "gentilicio" : "rondeño", "Monumento_hitorico" : "Punte del Tajo" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5a"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Olvera", "habitantes" : "8.124", "gentilicio" : "olvereño", "Monumento_hitorico" : "Castillo de Olvera" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5b"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Tarifa", "habitantes" : "18.169", "gentilicio" : "tarifeño", 
"Monumento_hitorico" : "Ruinas romanas de Baelo Claudia" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5c"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Zahara de la sierra", "habitantes" : "1.400", "gentilicio" : 
"zahareño", "Monumento_hitorico" : "Iglesia mayor" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5d"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Utrera", "habitantes" : "52.617", "gentilicio" : "utrerano", "Monumento_hitorico" : "Iglesia Santa Maria de la Mesa" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5e"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Los Palacios", "habitantes" : "38.246", "gentilicio" : "palaciegos", "Monumento_hitorico" : "Parroquia Mayor" }
Type "it" for more

// La consulta del $not, $gt es para discriminar a todas los pueblos que tengan mas habitantes de 10.000

> db.regex.find( { "habitantes": { $not: { $gt: 10.000 } } } )  
{ "_id" : ObjectId("5fa990c8407e64eed96b0804"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Dos hermanas", "habitantes" : "130.000", "gentilicio" : "nazareno", "Monumento_hitorico" : "Alqueria del Pilar" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0805"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Seteneil de las bodegas", "habitantes" : "2.769", "gentilicio" : "setenileño", "Monumento_hitorico" : "Fortaleza Nazari" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0806"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Ronda", "habitantes" : "34.000", "gentilicio" : "rondeño", "Monumento_hitorico" : "Punte del Tajo" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0807"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Olvera", "habitantes" : "8.124", "gentilicio" : "olvereño", "Monumento_hitorico" : "Castillo de Olvera" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0808"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Tarifa", "habitantes" : "18.169", "gentilicio" : "tarifeño", 
"Monumento_hitorico" : "Ruinas romanas de Baelo Claudia" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0809"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Zahara de la sierra", "habitantes" : "1.400", "gentilicio" : 
"zahareño", "Monumento_hitorico" : "Iglesia mayor" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080a"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Utrera", "habitantes" : "52.617", "gentilicio" : "utrerano", "Monumento_hitorico" : "Iglesia Santa Maria de la Mesa" }
Type "it" for more
> it
{ "_id" : ObjectId("5fa990c8407e64eed96b080b"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Los Palacios", "habitantes" : "38.246", "gentilicio" : "palaciegos", "Monumento_hitorico" : "Parroquia Mayor" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080c"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Moron de la Frontera", "habitantes" : "27.844", "gentilicio" : "moronero", "Monumento_hitorico" : "Castillo arabe" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080d"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Carmona", "habitantes" : "28.620", "gentilicio" : "carmonense", "Monumento_hitorico" : "Necropolis romana" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080e"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Conil de la frontera", "habitantes" : "22.427", "gentilicio" 
: "cooleño", "Monumento_hitorico" : "Iglesia de Santa Catalina" }
{ "_id" : ObjectId("5fa990c8407e64eed96b080f"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Vejer de la frontera", "habitantes" : "12.739", "gentilicio" 
: "vejeriego", "Monumento_hitorico" : "Torre del Mayorazgo" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0810"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Marbella", "habitantes" : "141.463", "gentilicio" : "marbelli", "Monumento_hitorico" : "Villa Romana" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0811"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Priego de Cordoba", "habitantes" : "22.285", "gentilicio" : "prieguense", "Monumento_hitorico" : "Iglesia de la Aurora" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0812"), "comunidad" : "Andalucia", "ciudad" : "Cordoba", "pueblo" : "Iznajar", "habitantes" : "4.343", "gentilicio" : "iznajeño", "Monumento_hitorico" : "Castillo de Iznajar" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0813"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Montefrio", "habitantes" : "5.479", "gentilicio" : "montefrieño", "Monumento_hitorico" : "El pateon y viejo cementerio" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0814"), "comunidad" : "Andalucia", "ciudad" : "Granada", "pueblo" : "Salobreña", "habitantes" : "12.396", "gentilicio" : "salobreño", "Monumento_hitorico" : "El castillo de Salobreña" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0815"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Andujar", "habitantes" : "37.113", "gentilicio" : "andujareño", "Monumento_hitorico" : "Basilica de Nuestra Señora de las Cabeza" }
{ "_id" : ObjectId("5fa990c8407e64eed96b0816"), "comunidad" : "Andalucia", "ciudad" : "Jaen", "pueblo" : "Baeza", "habitantes" : "15.902", "gentilicio" : "baezano", "Monumento_hitorico" : "La plaza de Santa Maria" }
{ "_id" : ObjectId("5fa9a453308668f49486fd57"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Dos hermanas", "habitantes" : "130.000", "gentilicio" : "nazareno", "Monumento_hitorico" : "Alqueria del Pilar" }
{ "_id" : ObjectId("5fa9a453308668f49486fd58"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Seteneil de las bodegas", "habitantes" : "2.769", "gentilicio" : "setenileño", "Monumento_hitorico" : "Fortaleza Nazari" }
{ "_id" : ObjectId("5fa9a453308668f49486fd59"), "comunidad" : "Andalucia", "ciudad" : "Malaga", "pueblo" : "Ronda", "habitantes" : "34.000", "gentilicio" : "rondeño", "Monumento_hitorico" : "Punte del Tajo" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5a"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Olvera", "habitantes" : "8.124", "gentilicio" : "olvereño", "Monumento_hitorico" : "Castillo de Olvera" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5b"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Tarifa", "habitantes" : "18.169", "gentilicio" : "tarifeño", 
"Monumento_hitorico" : "Ruinas romanas de Baelo Claudia" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5c"), "comunidad" : "Andalucia", "ciudad" : "Cadiz", "pueblo" : "Zahara de la sierra", "habitantes" : "1.400", "gentilicio" : 
"zahareño", "Monumento_hitorico" : "Iglesia mayor" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5d"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Utrera", "habitantes" : "52.617", "gentilicio" : "utrerano", "Monumento_hitorico" : "Iglesia Santa Maria de la Mesa" }
{ "_id" : ObjectId("5fa9a453308668f49486fd5e"), "comunidad" : "Andalucia", "ciudad" : "Sevilla", "pueblo" : "Los Palacios", "habitantes" : "38.246", "gentilicio" : "palaciegos", "Monumento_hitorico" : "Parroquia Mayor" }
Type "it" for more