# 📊 Sistema de Información Empresarial Mexicano (SIEM)
# Análisis Empresaral Mexicano SIEM 2024

---

## 📚 Tabla de Contenidos

- [🎯 Propósito](#-propósito)
- [📦 Conjunto de Datos](#-conjunto-de-datos)
- [🧪 Desarrollo del Proyecto](#-desarrollo-del-proyecto)
- [📈 Conclusiones y Recomendaciones](#-conclusiones-y-recomendaciones)
- [🛠️ Tecnologías](#-tecnologías)
- [⚙️ Instalación](#-instalación)
- [👤 Autores](#-autores)

---

## 🎯 Propósito

Analizar la distribución y características de las empresas registradas en el Sistema de Información Empresarial Mexicano (SIEM) para obtener insights sobre su localización, tamaño, sector económico predominante y diferencias regionales, usando técnicas estadísticas y visualización de datos.

---

## 📦 Conjunto de Datos

El conjunto de datos utilizado contiene las siguientes columnas:

- `_id`: Identificador único del registro	
- `razon_social`: Nombre de la empresa o establecimiento
- `estado`: Estado de la República Mexicana	
- `municipio`: Municipio del establecimiento	
- `domicilio`: Dirección completa	
- `colonia`: Colonia donde se ubica el establecimiento
- `cp`: Código postal
- `telefono`: Teléfono de contacto
- `e_mail`: Correo electrónico de contacto
- `giro`: Giro comercial o actividad económica principal
- `scian`: Código SCIAN correspondiente al giro
- `rango_de_empleados`: Rango estimado de empleados en el establecimiento
- `registrado_por`: Organización o cámara que registró el negocio
- `fn_razon_social`: Nombre comercial final, si aplica
- `fn_telefono`: Teléfono adicional o actualizado
- `fn_e_mail`: Correo electrónico adicional o actualizado
- `fn_giro`: Giro comercial final corregido, si aplica
- `estado_etq`: Etiqueta o formato estándar del estado (Ej. Estado de México)


Fuente: [!Datos.gob]https://www.datos.gob.mx/dataset/sistema_informacion_empresarial_mexicano.

---

## 🧪 Desarrollo del Proyecto

### **Carga y exploración inicial de los datos**:
El proyecto comenzó con la obtención del conjunto de datos sobre el Sistema de Información Empresarial en Mexicano, publicado en Datos.gob por la Secretaría de Economía (SE). Se realizó una exploración preliminar para entender la estructura del dataset, la cantidad de registros, las variables disponibles, y la granularidad temporal y geográfica. Esta fase incluyó el uso de funciones como .head(), .info() y .describe() para detectar inconsistencias básicas y comprender las dimensiones generales del problema.

Se identificaron valores nulos en las columnas: telefono, e_mail, giro, fn_razon_social, fn_telefono, fn_e_mail y  fn_giro.
```python 
print('Valores nulos por columnas')
valores_nulos = df_siem.isnull().sum()
print(valores_nulos)
```
```bash
Valores nulos por columnas
razon_social              71
estado                     0
municipio                  0
domicilio                  0
colonia                    0
cp                         0
telefono               34331
e_mail                 59180
giro                     257
scian                      0
rango_de_empleados         0
registrado_por             0
fn_razon_social       147849
fn_telefono            34353
fn_e_mail             147832
fn_giro               147694
estado_etq                 0
dtype: int64
```
Se identificaron valores duplicados en varias columnas:
```python
for nombre_columna in df_siem.columns:
    valores_duplicados = df_siem[nombre_columna].duplicated().sum()
    print(f'Valores duplicados en la columna {nombre_columna:<20}{valores_duplicados}')
    print('-' * 60)
```
```bash
Valores duplicados en la columna razon_social        33812
------------------------------------------------------------
Valores duplicados en la columna estado              147819
------------------------------------------------------------
Valores duplicados en la columna municipio           146712
------------------------------------------------------------
Valores duplicados en la columna domicilio           10739
------------------------------------------------------------
Valores duplicados en la columna colonia             117825
------------------------------------------------------------
Valores duplicados en la columna cp                  136820
------------------------------------------------------------
Valores duplicados en la columna telefono            71874
------------------------------------------------------------
Valores duplicados en la columna e_mail              89647
------------------------------------------------------------
Valores duplicados en la columna giro                116164
------------------------------------------------------------
Valores duplicados en la columna scian               147171
------------------------------------------------------------
Valores duplicados en la columna rango_de_empleados  147847
------------------------------------------------------------
Valores duplicados en la columna registrado_por      147703
------------------------------------------------------------
Valores duplicados en la columna fn_razon_social     147848
------------------------------------------------------------
Valores duplicados en la columna fn_telefono         71901
------------------------------------------------------------
Valores duplicados en la columna fn_e_mail           147849
------------------------------------------------------------
Valores duplicados en la columna fn_giro             147806
------------------------------------------------------------
Valores duplicados en la columna estado_etq          147819
------------------------------------------------------------
```
Para estos valores duplicados en la face de limpieza se explorara más a profundidad.


***Archivo: 1_eda.ipynb***

### **Limpieza y preprocesamiento**:
En esta fase de limpieza y preprocesamiento de los datos se realizó los siguientes pasos:

Verificamos la cantidad de filas y columnas de los datos:
```python
filas, columnas = df_siem.shape
print(f'{"Filas":<10}{"Columnas"}')
print(f'{filas:<10}{columnas:>7}')
```
```bash
Filas     Columnas
147851         17
```

Eliminamos las columnas innecesarias para el análisis:
```python
columnas_eliminar = ['cp','telefono', 'e_mail', 'fn_telefono', 'fn_e_mail', 'fn_razon_social', 'fn_giro', 'estado_etq']
n = 1

print('Columnas antes de eliminar')
for nombre_columnas in df_siem.columns:
    print(f'{n}.-{nombre_columnas}')
    n += 1

df_siem.drop(columnas_eliminar, axis=1, inplace=True)

print('\nColumnas después de eliminar')
i = 1 
for columna_nmombre in df_siem.columns:
    print(f'{i}.-{columna_nmombre}')
    i += 1
```
```bash
Columnas antes de eliminar
1.-razon_social
2.-estado
3.-municipio
4.-domicilio
5.-colonia
6.-cp
7.-telefono
8.-e_mail
9.-giro
10.-scian
11.-rango_de_empleados
12.-registrado_por
13.-fn_razon_social
14.-fn_telefono
15.-fn_e_mail
16.-fn_giro
17.-estado_etq

Columnas después de eliminar
1.-razon_social
2.-estado
3.-municipio
4.-domicilio
5.-colonia
6.-giro
7.-scian
8.-rango_de_empleados
9.-registrado_por
```
Se eliminaron 8 columnas.

Se eliminaron valores nulos:
```python
print('Filas antes de eliminar valores nulos')
print(f'Filas: {filas}')


print('\nFilas después de eliminar valores nulos')
df_siem_sin_nulos = df_siem.dropna()
filas_n, columnas_n = df_siem_sin_nulos.shape
print(f'Filas: {filas_n}')
```
```bash
Filas antes de eliminar valores nulos
Filas: 147851

Filas después de eliminar valores nulos
Filas: 147523
```

Para abordar los valores duplicados, se optó por analizar y detectar las filas duplicadas. Se comprendía que la duplicación de valores es posible, por lo que el objetivo fue identificar la redundancia a nivel de registro:
```python
filas_duplicadas = df_siem_sin_nulos.duplicated().sum()
filas_duplicadas_mask = df_siem_sin_nulos.duplicated()


print(f'Numero total de duplicados: {filas_duplicadas}')

df_siem_sin_nulos_duplicados = df_siem_sin_nulos[filas_duplicadas_mask]
df_siem_sin_nulos_duplicados.head(5)
```
```bash
Numero total de duplicados: 497
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>razon_social</th>
      <th>estado</th>
      <th>municipio</th>
      <th>domicilio</th>
      <th>colonia</th>
      <th>giro</th>
      <th>scian</th>
      <th>rango_de_empleados</th>
      <th>registrado_por</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1180</th>
      <td>NUEVA WALMART DE MEXICO S DE RL DE CV</td>
      <td>México</td>
      <td>Tlalnepantla de Baz</td>
      <td>Avenida HIDALGO S/N int NA</td>
      <td>Colonia INDUSTRIAL TLAXCOLPAN</td>
      <td>TIENDA DE CONVENIENCIA</td>
      <td>462111</td>
      <td>11 a 50</td>
      <td>CANACO SERVYTUR TLALNEPANTLA</td>
    </tr>
    <tr>
      <th>4450</th>
      <td>TESILLO</td>
      <td>México</td>
      <td>Zumpango</td>
      <td>Calle MINA 56 int SN</td>
      <td>Barrio SAN JUAN</td>
      <td>PAPELERIA</td>
      <td>465311</td>
      <td>0 a 10</td>
      <td>CANACO SERVYTUR CUAUTITLAN ZUMPANGO</td>
    </tr>
    <tr>
      <th>4710</th>
      <td>hules angel</td>
      <td>México</td>
      <td>Cuautitlán Izcalli</td>
      <td>Privada rio concepcion sn int sn</td>
      <td>Colonia colinas del lago</td>
      <td>hule automotriz e industrial</td>
      <td>468211</td>
      <td>0 a 10</td>
      <td>CANACO SERVYTUR CUAUTITLAN ZUMPANGO</td>
    </tr>
    <tr>
      <th>5260</th>
      <td>JIMENEZ</td>
      <td>Michoacán de Ocampo</td>
      <td>Contepec</td>
      <td>Calle N/A N/A int NA</td>
      <td>Colonia N/A</td>
      <td>COMERCIO</td>
      <td>461110</td>
      <td>0 a 10</td>
      <td>CANACO SERVYTUR MORELIA</td>
    </tr>
    <tr>
      <th>5673</th>
      <td>AGUILAR</td>
      <td>Michoacán de Ocampo</td>
      <td>Maravatío</td>
      <td>Calle San Francisco N/A int N/A</td>
      <td>Colonia N/A</td>
      <td>ABARROTES</td>
      <td>431110</td>
      <td>0 a 10</td>
      <td>CANACO SERVYTUR MORELIA</td>
    </tr>
  </tbody>
</table>
</div>
```

3. **Análisis exploratorio de datos (EDA)**:
   - [Ej. Distribución, correlaciones, agrupaciones, etc.]

4. **Visualización de datos**:
   - Uso de gráficos de barras, líneas, cajas, dispersión y mapas de calor.

5. **Modelado o reportes (opcional)**:
   - [Si aplica: modelos de ML, clustering, predicciones, etc.]

6. **Conclusiones y recomendaciones**:
   - Síntesis de hallazgos clave y propuestas de acción.

---

## 📈 Conclusiones y Recomendaciones

- [Insight 1]
- [Insight 2]
- [Recomendación práctica o estratégica basada en los datos]

---

## 🛠️ Tecnologías

- Python
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook / Google Colab
- [Otras herramientas que uses, como Scikit-learn, Plotly, etc.]

---

## ⚙️ Instalación

### 1. Clonar este repositorio:
```bash
git clone https://github.com/tu_usuario/nombre_del_proyecto.git
```
### 2. Uso de un Entorno Virtual para Aislar Dependencias

Para evitar conflictos con versiones de librerías, se recomienda usar entornos virtuales.

####  Crear y Activar un Entorno Virtual

##### Crear el entorno virtual:
```
python -m venv venv
```
##### Activar el entorno:
* #### En Windows:

    ```
    venv\Scripts\activate
    ```

* #### En Mac/Linux::

    ```
    source venv/bin/activate
    ```
#### 3. Instalar dependencias dentro del entorno:
* #### Opición 1:
    ```
    pip install -r requirements.txt
    ```

* #### Opción 2 (De forma manual):
    ```
    pip install numpy pandas matplotlib seaborn scikit-learn
    ```
---

## 👤 Autor

**Said Mariano Sánchez** – *smariano170@gmail.com*  
Este proyecto forma parte de mi portafolio como analista de datos Jr.

---

## 📝 Licencia

Este proyecto está licenciado bajo la **Licencia MIT**. Puedes usarlo, modificarlo y distribuirlo libremente, siempre que menciones al autor original.

---