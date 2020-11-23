# Link de descarga de los videos

https://we.tl/t-sPDEoIiGnN 

# **Introducción a R.**
*Dr. Edmundo Molina, Victor Espinoza* 

En este laboratorio, introduciremos algunos comandos simples de R. La mejor manera de aprender un nuevo lenguaje es probando los comandos. R y RStudio pueden ser descargados de

http://cran.r-project.org/

https://rstudio.com/products/rstudio/download/

## 1. Comandos básicos

R utiliza funciones para realizar operaciones. Para ejecutar una función llamada _funcname_, escribimos funcname(input1, input2), donde las entradas (o argumentos) input1 y input2 le dicen a R cómo ejecutar la función. Una función puede tener cualquier número de argumentos. Por ejemplo, para crear un vector de números, usamos la función c() (para concatenar). Cualquier número dentro de los paréntesis se unen entre sí. El siguiente comando instruye a R para que junte los números 1, 3, 2 y 5, y los guarde como un vector llamado x. Cuando tecleamos x, nos devuelve el vector.

```{r}
x<-c(1,3,2,5)
x
```

También podemos guardar cosas usando = en lugar de <-:

```{r}
x=c(1,6,2)
x
y=c(1,4,3)
y
```

Si se escribe ?funcname, R abrirá siempre una nueva ventana de ayuda con información adicional sobre la función funcname.

Podemos decirle a R que sume dos conjuntos de números. Entonces sumará el primer número de x al primer número de y, y así sucesivamente. Sin embargo, x y y deberían tener la misma longitud. Podemos comprobar su longitud usando la función length().

```{r}
?length
length (x)
length (y)
x+y
```

La función ls() nos permite ver una lista de todos los objetos, como datos y funciones, que hemos guardado hasta ahora. La función rm() puede ser usada para borrar cualquiera que no queramos.

```{r}
ls()
rm(x,y)
ls()
```

También es posible retirar todos los objetos a la vez:

```{r}
rm(list=ls())
```

La función matrix() puede ser usada para crear una matriz de números. Antes de usar la función matrix(), podemos aprender más sobre ella:

```{r}
?matrix
```

El archivo de ayuda revela que la función matrix() toma un número de entradas, pero por ahora nos centramos en las tres primeras: los datos (las entradas en la matriz), el número de filas y el número de columnas. Primero, creamos una matriz simple.

```{r}
x<-matrix (data=c(1,2,3,4), nrow=2, ncol=2)
x
```

Note que podríamos omitir el teclear data=, nrow=, y ncol= en el comando matrix() de arriba: es decir, podríamos simplemente teclear

```{r}
x<-matrix (c(1,2,3,4), 2, 2)
x
```

y esto tendría el mismo efecto. Sin embargo, a veces puede ser útil especificar los nombres de los argumentos que se pasan, ya que de lo contrario R asumirá que los argumentos de la función se pasan a la función en el mismo orden que se da en el archivo de ayuda de la función. Como ilustra este ejemplo, por defecto R crea matrices rellenando sucesivamente las columnas. Alternativamente, se puede utilizar la opción byrow=TRUE para rellenar la matriz en el orden de las filas.

```{r}
matrix (data=c(1,2,3,4) , nrow=2, ncol =2,byrow =TRUE)
```

Observe que en el comando anterior no asignamos la matriz a un valor como x. En este caso la matriz se imprime en la pantalla pero no se guarda para futuros cálculos. La función sqrt() devuelve la raíz cuadrada de cada elemento de un vector o matriz. El comando x^2 eleva cada elemento de x a la potencia 2; cualquier potencia es posible, incluyendo las potencias fraccionarias o negativas.

```{r}
sqrt(x)
x^2
```

La función rnorm() genera un vector de variables normales aleatorias, con el primer argumento n el tamaño de la muestra. Cada vez que llamemos a esta función, obtendremos una respuesta diferente. Aquí creamos dos conjuntos de números correlacionados, x e y, y usamos la función cor() para calcular la correlación entre ellos.

```{r}
x=rnorm (50)
y=x+rnorm (50, mean=50, sd=.1)
cor(x,y)
```

Por defecto, rnorm() crea variables aleatorias normales estándar con una media de 0 y una desviación estándar de 1. Sin embargo, la media y la desviación estándar pueden ser alteradas usando los argumentos mean y sd, como se ilustra arriba. A veces queremos que nuestro código reproduzca exactamente el mismo conjunto de números aleatorios; podemos utilizar la función set.seed() para hacerlo. La función set.seed() toma un argumento entero (arbitrario).

```{r}
set.seed (1303)
rnorm (50)
```

Utilizamos set.seed() en todos los laboratorios siempre que realizamos cálculos que implican cantidades aleatorias. En general, esto debería permitir al usuario reproducir nuestros resultados. Sin embargo, debe tenerse en cuenta que a medida que se disponga de nuevas versiones de R es posible que se formen algunas pequeñas discrepancias entre el libro y la salida de R.

Las funciones mean() y var() pueden utilizarse para calcular la media y la varianza de un vector de números. Aplicando sqrt() a la salida de var() se obtendrá la desviación estándar. O simplemente podemos usar la función sd().

```{r}
set.seed (3)
y=rnorm (100)
mean(y)
var(y)
sqrt(var(y))
sd(y)
```

## 2. Gráficas

La función plot() es la forma principal de representar los datos en R. Por ejemplo, plot(x,y) produce un diagrama de dispersión de los números en x frente a los números en y. Hay muchas opciones adicionales que pueden pasarse a la función plot(). Por ejemplo, si se pasa el argumento xlab se obtendrá una etiqueta en el eje x. Para obtener más información sobre la función plot(), escribe ?plot.

```{r}
x=rnorm (100)
y=rnorm (100)
plot(x,y)
plot(x,y,xlab="Este es el eje x",ylab="Este es el eje y",
main="Plot de X vs Y")
```

A menudo querremos guardar la salida de un plot en R. El comando que usamos para hacerlo dependerá del tipo de archivo que queramos crear. Por ejemplo, para crear un pdf, usamos la función pdf(), y para crear un jpeg, usamos la función jpeg().

```{r}
pdf ("Figure.pdf")
plot(x,y,col ="green")
dev.off ()
```

La función dev.off() indica a R que hemos terminado de crear el plot. Alternativamente, podemos simplemente copiar la ventana del gráfico y pegarla en un tipo de archivo apropiado, como un documento de Word.

La función seq() puede ser usada para crear una secuencia de números. Por ejemplo, seq(a,b) hace un vector de números enteros entre a y b. Hay muchas otras opciones: por ejemplo, seq(0,1,length=10) hace una secuencia de 10 números que están igualmente espaciados entre 0 y 1. Escribir 3:11 es una forma abreviada de seq(3,11) para argumentos de números enteros.

```{r}
x<-seq (1 ,10)
x
x<-1:10
x
x<-seq(-pi ,pi ,length =50)
x
```

Ahora crearemos algunos ploteos más sofisticados. La función contour() produce un gráfico de contorno para representar datos tridimensionales; es como un mapa topográfico. Requiere tres argumentos:

1. Un vector de los valores x (la primera dimensión),

2. Un vector de los valores y (la segunda dimensión), y

3. Una matriz cuyos elementos corresponden al valor z (la tercera dimensión) para cada par de coordenadas (x,y).

Al igual que con la función plot(), hay muchas otras entradas que pueden utilizarse para afinar la salida de la función contour(). Para aprender más sobre ellas, eche un vistazo al archivo de ayuda escribiendo ?contour.

```{r}
y<-x
f<-outer(x,y,function (x,y)cos(y)/(1+x^2))
contour (x,y,f)
contour (x,y,f,nlevels =45, add=T)
fa<-(f-t(f))/2
contour (x,y,fa,nlevels =15)
```

La función image() funciona de la misma manera que contour(), excepto que produce un gráfico codificado por colores cuyos colores dependen del valor de z. Esto se conoce como un mapa de calor, y a veces se utiliza para trazar la temperatura en los pronósticos del tiempo. Alternativamente, persp() puede ser usada para producir un gráfico tridimensional. Los argumentos theta y phi controlan los ángulos en los que se visualiza el gráfico.

```{r}
image(x,y,fa)
persp(x,y,fa)
persp(x,y,fa ,theta =30)
persp(x,y,fa ,theta =30, phi =20)
persp(x,y,fa ,theta =30, phi =70)
persp(x,y,fa ,theta =30, phi =40)
```

## 3. Indexación de datos

A menudo deseamos examinar parte de un conjunto de datos. Supongamos que nuestros datos están almacenados en la matriz A.

```{r}
A<-matrix (1:16 ,4 ,4)
A
```

Luego, tecleando:

```{r}
A[2,3]
```

seleccionará el elemento correspondiente a la segunda fila y la tercera columna. El primer número después del símbolo de paréntesis abierto [ se refiere siempre a la fila, y el segundo número se refiere siempre a la columna. También podemos seleccionar varias filas y columnas a la vez, proporcionando vectores como los índices.

```{r}
A[c(1,3) ,c(2,4) ]
A[1:3 ,2:4]
A[1:2 ,]
A[ ,1:2]
```

Los dos últimos ejemplos incluyen la ausencia de índice para las columnas o la ausencia de índice para las filas. Estos indican que R debe incluir todas las columnas o todas las filas, respectivamente. R trata una sola fila o columna de una matriz como un vector.

```{r}
A[1,]
```

El uso de un signo negativo - en el índice le dice a R que mantenga todas las filas o columnas excepto las indicadas en el índice.

```{r}
A[-c(1,3) ,]
A[-c(1,3) ,-c(1,3,4)]
```

La función dim() da como resultado el número de filas seguido por el número de columnas de una matriz dada.

```{r}
dim(A)
```

## 4. Carga de datos

Para la mayoría de los análisis, el primer paso consiste en importar un conjunto de datos a R. La función read.table() es una de las principales formas de hacerlo. El archivo de ayuda contiene detalles sobre cómo utilizar esta función. Podemos usar la función write.table() para exportar datos.

Antes de intentar cargar un conjunto de datos, debemos asegurarnos de que R sepa buscar los datos en el directorio apropiado. 

La manera más sencilla de hacerlo es mediante la función setwd y en la que asignaremos la carpeta en la que vamos a estar trabajando

```{r}
setwd("C:/Users/User.HPPROBOOK640G1/Google Drive/DPP/Apoyo cursos/R para maestría")
```

Ahora comenzamos cargando el conjunto de datos de Auto. Estos datos son parte de la biblioteca de ISLR (discutimos las bibliotecas un poco más hacia el final del este curso) pero para ilustrar la función read.table() los cargamos ahora desde un archivo de texto. El siguiente comando cargará el archivo Auto.data en R y lo almacenará como un objeto llamado Auto, en un formato llamado marco de datos. (El archivo de texto se puede obtener en la siguiente dirección [https://github.com/vespinozaj/Intro_R](https://github.com/vespinozaj/Intro_R) y se deberá guardar en la carpeta en la que se estableción el directorio de trabajo). Una vez que se han cargado los datos, se pueden previsualizar en RStudio.

```{r}
Auto<-read.table("Auto.data.txt")
head(Auto)
View(Auto)
```

Tenga en cuenta que Auto.data es simplemente un archivo de texto, que puede abrir en su computadora usando un editor de texto estándar. A menudo es una buena idea ver un conjunto de datos utilizando un editor de texto u otro software como Excel antes de cargarlo en R.

Este conjunto de datos en particular no se ha cargado correctamente, porque R ha asumido que los nombres de las variables forman parte de los datos y por lo tanto los ha incluido en la primera fila. El conjunto de datos también incluye una serie de observaciones que faltan, indicadas por un signo de interrogación ?. Los valores faltantes son comunes en los conjuntos de datos reales. El uso de la opción header=T (o header=TRUE) en la función read.table() le dice a R que la primera línea del archivo contiene los nombres de las variables, y el uso de la opción na.strings le dice a R que cada vez que vea un determinado carácter o conjunto de caracteres (como un signo de interrogación), debe tratarse como un elemento faltante de la matriz de datos.

```{r}
Auto<-read.table ("Auto.data.txt", header =T,na.strings ="?")
head(Auto)
View(Auto)
```

Excel es un programa de almacenamiento de datos de formato común. Una forma fácil de cargar esos datos en R es guardarlos como un archivo csv (valor separado por comas) y luego usar la función read.csv() para cargarlos.

```{r}
Auto<-read.csv("Auto.csv", header =T,na.strings ="?")
head(Auto)
dim(Auto)
Auto[1:4 ,]
```

La función dim() nos dice que los datos tienen 397 observaciones, o filas, y nueve variables, o columnas. Hay varias maneras de tratar los datos que faltan. En este caso, sólo cinco de las filas contienen observaciones faltantes, y por lo tanto elegimos usar la función na.omit() para simplemente eliminar estas filas.

```{r}
Auto<-na.omit(Auto)
dim(Auto)
```

Una vez que los datos se cargan correctamente, podemos usar names() para comprobar los nombres de las variables.

```{r}
names(Auto)
```

## 5. Resúmenes gráficos y numéricos adicionales

Podemos usar la función plot() para producir gráficos de dispersión de las variables cuantitativas. Sin embargo, con sólo teclear los nombres de las variables se producirá un mensaje de error, ya que R no sabe buscar en el conjunto de datos de Auto para esas variables.

```{r}
#plot(cylinders, mpg)
```

Para referirse a una variable, debemos escribir el conjunto de datos y el nombre de la variable unidos con un símbolo $. Alternativamente, podemos usar la función attach() para decirle a R que haga que las variables de este marco de datos estén disponibles por nombre.

```{r}
plot(Auto$cylinders , Auto$mpg )
attach (Auto)
plot(cylinders , mpg)
```

La variable de los cilindros se almacena como un vector numérico, por lo que R la ha tratado como cuantitativa. Sin embargo, como sólo hay un pequeño número de valores posibles para los cilindros, se puede preferir tratarla como una variable cualitativa. La función as.factor() convierte las variables cuantitativas en variables cualitativas.

```{r}
cylinders <-as.factor (cylinders)
```

Si la variable trazada en el eje x es categórica, entonces los boxplots se producirán automáticamente por la función plot(). Como de costumbre, se pueden especificar varias opciones para personalizar los gráficos.

```{r}
plot(cylinders , mpg)
plot(cylinders , mpg , col ="red ")
plot(cylinders , mpg , col ="red", varwidth =T)
plot(cylinders , mpg , col ="red", varwidth =T,horizontal =T)
plot(cylinders , mpg , col ="red", varwidth =T, xlab=" cylinders ",
ylab ="MPG ")
```

La función hist() puede usarse para trazar un histograma. Observe que col=2 tiene el mismo efecto que col="red".

```{r}
hist(mpg)
hist(mpg ,col =2)
hist(mpg ,col =2, breaks =15)
```

La función pairs() crea una matriz de diagramas de dispersión, es decir, un diagrama de dispersión para cada par de variables de un determinado subconjunto de datos.

```{r}
pairs(~ mpg + displacement + horsepower + weight + acceleration, Auto)
```

Junto con la función plot(), identify() proporciona un método interactivo útil para identificar el valor de una determinada variable para los puntos de un gráfico. Pasamos tres argumentos para identificar(): la variable del eje x, la variable del eje y y la variable cuyos valores queremos ver impresos para cada punto. Luego, al hacer clic en un punto dado del gráfico, R imprimirá el valor de la variable de interés.

```{r}
plot(horsepower ,mpg)
identify (horsepower ,mpg ,name)
```

La función summary() produce un resumen numérico de cada variable de un determinado conjunto de datos.

```{r}
summary (Auto)
```

En el caso de las variables cualitativas, como el nombre, R enumerará el número de observaciones que corresponden a cada categoría. También podemos producir un resumen de una sola variable.

```{r}
summary (mpg)
```

## 6. Librerías

La función **library()** se utiliza para cargar librerias, o grupos de funciones y conjuntos de datos que no están incluidos en la distribución de la base R. Funciones básicas que realizan una regresión lineal de mínimos cuadrados y otros análisis simples vienen de manera estándar en R, pero las funciones más exóticas o especializadas requieren librerías adicionales. Aquí cargamos la librería **MASS**, que es una gran la recopilación de conjuntos de datos y funciones. También cargamos la librería **ISLR**, que incluye los conjuntos de datos asociados a este libro.

```{r}
library (MASS)
library (ISLR)
```

Si recibe un mensaje de error al cargar cualquiera de estas librerías,  probablemente indica que la librería correspondiente no ha sido instalada todavía en tu sistema. Algunas bibliotecas, como **MASS**, vienen con **R** y no necesitan se instalen por separado en su ordenador. Sin embargo, otros paquetes, como **ISLR**, deben ser descargados la primera vez que se usen. Esto puede hacerse en la línea de comandos R mediante **install.packages("ISLR")**. Esta instalación sólo tiene que hacerse la primera vez que se usa un paquete. Sin embargo, la función library() debe ser llamada cada vez que se desee utilizar un determinado paquete.

## 7. Escribir Funciones

Como hemos visto, **R** viene con muchas funciones útiles, y aún más funciones están disponibles a través de las bibliotecas **R**. Sin embargo, a menudo estaremos interesados en la realización de una operación para la que no se dispone de ninguna función. En este caso es posible que queramos escribir nuestra propia función. Por ejemplo, debajo de nosotros proporcionan una simple función que se lee en las librerías de **ISLR** y **MASS**, llamada **LoadLibraries()**. Antes de que hayamos creado la función, **R** devuelve un error si tratamos de llamarlo.

```{r eval=FALSE, include=TRUE}
LoadLibraries
LoadLibraries()
```
Ahora creamos la función. Observe que los símbolos **+** son impresos por **R** y no deben ser escritos en la sintaxis de la función. El símbolo **{** informa a **R** que los múltiples comandos están a punto de ser introducidos. Al pulsar Enter después de escribir **{** hará que **R** imprima el símbolo **+**. Podemos entonces introducir tantos comandos como queramos, pulsando Enter después de cada uno. Finalmente el símbolo **}** informa a **R** que no hay más órdenes para ser ingresadas.

```{r}
LoadLibraries<-function(){ 
  library(ISLR) ;
  library(MASS) ;
  print("The libraries have been loaded.")}
```

Ahora, si tecleamos **LoadLibraries**, **R** nos dirá qué hay en la función.

```{r}
LoadLibraries
```

Si llamamos a la función, las bibliotecas se cargan y la declaración de impresión es la salida.

```{r eval=FALSE, include=TRUE}
LoadLibraries()
```

Crear una función que muestra un mensaje que recibe como argumento

```{r}
fn.showmsg <- function(msg) {
  msg
}
fn.showmsg("Este es el mensaje que se va a mostrar")
```

Crear un data frame y después llamar a la funcion fn.showmsg

```{r}
datos<-data.frame(nombres = c("Oscar", "Paty", "Lulu"), edades = c(20,34,56))
fn.showmsg(datos)
```
