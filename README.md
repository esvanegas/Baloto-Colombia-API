# Baloto API

El presente repositorio tiene como objetivo presentar algunos de los tipos de da información disponibles para consultar, así como mostrar la funcionalidad de estos para obtener datos del juego de azar colombiano _Baloto - Revancha_

Cabe aclarar que esta documentacion _**NO**_ es información oficial, la información expresada a continuación se obtuvo realizando ingeniería inversa a la página oficial del baloto - [www.baloto.com](https://www.baloto.com).

# Indice

1. [Información general](#general)
    - [Tipos de consulta](#types)
        - /LastGameResult
        - /GameResultByDate
        - /GameWithCondition

2. [Response Objects](#resObjs)
    - [Game Result Object](#GameResult)

<a href="general"></a>

# Información General

Todas las peticiones deben de enviarse mediante método **POST** hacia el host [https://api-baloto-prod.baloto.com/petition](https://api-baloto-prod.baloto.com/petition)

El objeto body de la solicitud debe de tener la siguiente estructura:

| Parametro | Descripción |
| --- | --- |
| `type` | Tipo de consulta a obtener |
| `parameters` | Parametros opcionales para filtrar según sql y graphql|

<a href="types"></a>

## Tipos de consulta:

Siendo así los tipos de consultas disponibles son:

- **_/LastGameResult:_**

    Obtiene el último resultado del juego del baloto.

    **Retorna**: `GameResult[]` - Resultado del juegos [GameResult](#GameResult).

    **Parametros disponibles del objeto `parameters`**:

    | Param | Formato | Ejemplo |
    | -- | -- | -- |
    | order | `SQL` | `sorteo DESC` |
    | limit | `number` | 1

    **EJEMPLO:**

    ```json
    {
        "type": "/LastGameResult",
        "parameters":{
            "order": "sorteo DESC",
            "limit": 1
        }
    }
    ```

    **NOTA:** _Para obtener los resultados de todos los juegos enviar el objeto del body sin el parametro `parameters`_

- **_/GameResultByDate:_**

    Obtiene los resultados de los juegos de un mes especifico

    **Retorna**: `GameResult[]` - Resultados de los juegos [GameResult](#GameResult).

    **Parametros disponibles del objeto Parameters**:

    | Param | Formato | Ejemplo |
    | -- | -- | -- |
    | gameDate | `YYYY/MM` | `2021/09` |

    **EJEMPLO:**
    
    ```json
    {
        "type": "/GameResultByDate",
        "parameters":{
            "gameDate": "2021/09"
        }
    }
    ```

- **_/GameWithCondition:_**

    Obtiene los resultados de los juegos con unas condiciones especificas

    **Retorna**: `GameResult[]` - Resultados de los juegos [GameResult](#GameResult).

    **Parametros disponibles del objeto Parameters**: No se mostrará una lista de parametros disponibles debido a que los filtros pueden llegar a ser muy complejos de estandarizar, por este motivo por favor guiarse del siguiente ejemplo:

    **EJEMPLO:**
    
    ```json
    {
        "type": "/GameWithCondition",
        "parameters":{
            "condition":{
                "where":{
                    "or":[{
                            "baloto_cayo":"S"
                        },
                        {
                            "revancha_cayo":"S"
                        }
                    ]
                }
            }
        }
    }


<a href="resObjs"></a>

## Response Objects

<a href="GameResult"></a>

### GameResult Object

Objeto de resultado de juego


| Parametro | Tipo | Descripción |
| --- | --- | --- |
| id | `number` | ID del juego |
| date | `Date` | Fecha del juego |
| video | `string` | URL del vídeo del sorteo |
| baloto_cayo | `string` | Cayó o no el baloto |
| baloto_ciudad | `string` | Ciudad donde cayó el baloto |
| revancha_cayo | `string` | Cayó o no la revancha |
| revancha_ciudad | `string` | Ciudad donde cayó el baloto |
| sorteo | `number` | Número del sorteo |
| baloto1 | `number` | Número de la primera balota ganadora del baloto|
| baloto2 | `number` | Número de la segunda balota ganadora del baloto|
| baloto3 | `number` | Número de la tercera balota ganadora del baloto de izquiera a derecha|
| baloto4 | `number` | Número de la cuarta balota ganadora del baloto |
| baloto5 | `number` | Número de la quinta balota ganadora del baloto|
| baloto6 | `number` | Número de la super balota ganadora del baloto|
| baloto_ganadores1 | `number` | # de Ganadores en primer nivel del baloto |
| baloto_ganadores1_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de primer nivel |
| baloto_ganadores2 | `number` | # de Ganadores en segundo nivel del baloto |
| baloto_ganadores2_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de segundo nivel |
| baloto_ganadores3 | `number` | # de Ganadores en tercer nivel del baloto |
| baloto_ganadores3_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de tercer nivel |
| baloto_ganadores4 | `number` | # de Ganadores en cuarto nivel del baloto |
| baloto_ganadores4_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de cuarto nivel |
| baloto_ganadores5 | `number` | # de Ganadores en quinto nivel del baloto |
| baloto_ganadores5_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de quinto nivel |
| baloto_ganadores6 | `number` | # de Ganadores en sexto nivel del baloto |
| baloto_ganadores6_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de sexto nivel |
| baloto_ganadores7 | `number` | # de Ganadores en séptimo nivel del baloto |
| baloto_ganadores7_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de séptimo nivel |
| baloto_ganadores8 | `number` | # de Ganadores en octavo nivel del baloto |
| baloto_ganadores8_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de octavo nivel |
| baloto_acumulado | `number` | Cantidad de dinero acumulado en el baloto (No muy seguro) |
| baloto_acumulado_real | `number` | Cantidad de dinero acumulado en el baloto (No muy seguro)|
| revancha1 | `number` | Número de la primera balota ganadora de la revancha|
| revancha2 | `number` | Número de la segunda balota ganadora de la revancha|
| revancha3 | `number` | Número de la tercera balota ganadora de la revancha|
| revancha4 | `number` | Número de la cuarta balota ganadora de la revancha|
| revancha5 | `number` | Número de la quinta balota ganadora de la revancha|
| revancha6 | `number` | Número de la super balota ganadora de la revancha|
| revancha_ganadores1 | `number` | # de Ganadores en primer nivel de la revancha |
| revancha_ganadores1_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de primer nivel |
| revancha_ganadores2 | `number` | # de Ganadores en segundo nivel de la revancha |
| revancha_ganadores2_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de segundo nivel |
| revancha_ganadores3 | `number` | # de Ganadores en tercer nivel de la revancha |
| revancha_ganadores3_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de tercer nivel |
| revancha_ganadores4 | `number` | # de Ganadores en cuarto nivel de la revancha |
| revancha_ganadores4_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de cuarto nivel |
| revancha_ganadores5 | `number` | # de Ganadores en quinto nivel de la revancha |
| revancha_ganadores5_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de quinto nivel |
| revancha_ganadores6 | `number` | # de Ganadores en sexto nivel de la revancha |
| revancha_ganadores6_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de sexto nivel |
| revancha_ganadores7 | `number` | # de Ganadores en séptimo nivel de la revancha |
| revancha_ganadores7_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de séptimo nivel |
| revancha_ganadores8 | `number` | # de Ganadores en octavo nivel de la revancha |
| revancha_ganadores8_valor | `number` | Cantidad de dinero en COP que le pertenece a cada ganador de octavo nivel |
| revancha_acumulado | `number` | Cantidad de dinero acumulado en la revancha (No muy seguro) |
| revancha_acumulado_real | `number` | Cantidad de dinero acumulado en la revancha (No muy seguro)|
| noticia | `string ó null` | URL de la noticia si hay |

### Ejemplo:

```json
{
    "id": 2129,
    "date": "2021-09-04T00:00:00.000Z",
    "video": "https://youtu.be/CaO9Pr4tm8E",
    "baloto_cayo": "N",
    "baloto_ciudad": "",
    "revancha_cayo": "N",
    "revancha_ciudad": "",
    "sorteo": 2117,
    "baloto1": 22,
    "baloto2": 30,
    "baloto3": 31,
    "baloto4": 34,
    "baloto5": 41,
    "baloto6": 16,
    "baloto_ganadores1": 0,
    "baloto_ganadores1_valor": 0,
    "baloto_ganadores2": 1,
    "baloto_ganadores2_valor": 47322206,
    "baloto_ganadores3": 5,
    "baloto_ganadores3_valor": 9484200,
    "baloto_ganadores4": 41,
    "baloto_ganadores4_valor": 10373328,
    "baloto_ganadores5": 119,
    "baloto_ganadores5_valor": 8990212,
    "baloto_ganadores6": 1960,
    "baloto_ganadores6_valor": 29341200,
    "baloto_ganadores7": 1780,
    "baloto_ganadores7_valor": 23433700,
    "baloto_ganadores8": 24954,
    "baloto_ganadores8_valor": 142237800,
    "baloto_acumulado": 31500000000,
    "baloto_acumulado_real": 31000000000,
    "revancha1": 8,
    "revancha2": 15,
    "revancha3": 30,
    "revancha4": 36,
    "revancha5": 41,
    "revancha6": 14,
    "revancha_ganadores1": 0,
    "revancha_ganadores1_valor": 0,
    "revancha_ganadores2": 1,
    "revancha_ganadores2_valor": 16649574,
    "revancha_ganadores3": 2,
    "revancha_ganadores3_valor": 3336868,
    "revancha_ganadores4": 65,
    "revancha_ganadores4_valor": 3649685,
    "revancha_ganadores5": 145,
    "revancha_ganadores5_valor": 3163030,
    "revancha_ganadores6": 2430,
    "revancha_ganadores6_valor": 10322640,
    "revancha_ganadores7": 1856,
    "revancha_ganadores7_valor": 8244352,
    "revancha_ganadores8": 20065,
    "revancha_ganadores8_valor": 42136500,
    "revancha_acumulado": 11500000000,
    "revancha_acumulado_real": 11000000000,
    "noticia": null
}
```