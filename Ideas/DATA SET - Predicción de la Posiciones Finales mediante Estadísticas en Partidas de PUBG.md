En la vida real, la industria de los videojuegos es uno de los campos que más contrata especialistas en Machine Learning y Ciencia de Datos. Lo que hace empresas como Tencent, Epic Games o Supercell para balancear sus juegos y emparejar a los jugadores es, literalmente, aplicar regresión multivariable sobre millones de datos de telemetría.



Y tienes toda la razón: como es un Battle Royale con exactamente 100 jugadores cayendo en un mapa simultáneamente, la complejidad matemática de predecir quién va a sobrevivir basándose en 29 variables cruzadas es altísima. Es un problema de optimización fascinante.





Nombre del Estudiante: Carlo Daniel Kevin Apaza Villca



Nombre del Dataset: Predicción de la Posiciones Finales mediante Estadísticas en Partidas de PUBG





Descripción del Dataset: Este conjunto de datos contiene el rastreo de datos reales e históricos de partidas de PUBG (PlayerUnknown's Battlegrounds), abarcando modalidades en solitario, dúos y escuadrones con hasta 100 agentes por sesión. Cuenta con más de un millón de filas (volumen que se alcanza al recopilar datos anónimos de más de 65.000 partidas, ya que al terminar cada sesión el servidor genera una fila individual con las estadísticas de cada agente). Estas estadísticas se desglosan en 29 columnas (características) que miden acciones detalladas como curaciones usadas, distancia recorrida, daño infligido y armas recogidas. En la materia de Inteligencia Artificial, esto se utilizará para aplicar regresión multivariable y predecir en qué puesto final terminará un agente (en una escala continua de 1.0 para el ganador a 0.0 para el último lugar) en función de dichas estadísticas.

URL del Dataset: https://www.kaggle.com/c/pubg-finish-placement-prediction/data





----------------------------------------------------------------------------------------------------------------------------------------------------------------



Identificadores y Datos de la Partida



&nbsp;	Id: El identificador único de cada 

&nbsp;	jugador.groupId: El identificador del grupo o equipo al que pertenece el jugador dentro de esa partida en 

&nbsp;	específico.matchId: El identificador único de la partida.

&nbsp;	matchDuration: La duración total de la partida, medida en segundos.

&nbsp;	matchType: Una cadena de texto que identifica el modo de juego (como solo, dúo, squad, o en primera persona como "solo-fpp").

&nbsp;	maxPlace: La peor posición registrada de toda la partida.

&nbsp;	numGroups: La cantidad de equipos o grupos diferentes presentes en la partida.



Acción y Combate

&nbsp;	kills: La cantidad total de jugadores enemigos eliminados por ese jugador.

&nbsp;	headshotKills: El número de esas eliminaciones logradas mediante tiros a la cabeza.

&nbsp;	roadKills: Los asesinatos cometidos mientras el jugador iba en un vehículo.

&nbsp;	teamKills: El número de veces que el jugador mató (accidental o intencionalmente) a un compañero de equipo.

&nbsp;	DBNOs: El número de enemigos que el jugador "noqueó" (es decir, tiró al suelo pero aún no murieron por completo).

&nbsp;	assists: La cantidad de enemigos a los que este jugador infligió daño, pero que terminaron siendo eliminados por sus propios compañeros.

&nbsp;	damageDealt: El daño total causado por el jugador, restando el daño que se pudo haber autoinfligido por error.

&nbsp;	longestKill: La distancia máxima (el tiro más largo) a la que mató a un enemigo en el momento de su muerte.

&nbsp;	killStreaks: El número máximo de enemigos asesinados en una ráfaga muy corta de tiempo.



Supervivencia y Estrategiaheals: La cantidad de artículos de curación básica utilizados.

&nbsp;	boosts: El número de artículos potenciadores (como bebidas energéticas) utilizados.

&nbsp;	revives: Las veces que el jugador revivió a un compañero caído en combate.

&nbsp;	weaponsAcquired: El número total de armas recogidas del suelo durante la partida.

&nbsp;	vehicleDestroys: La cantidad de vehículos que el jugador logró hacer explotar.



Movimiento (Posicionamiento)

&nbsp;	walkDistance: La distancia total viajada a pie, en metros.

&nbsp;	rideDistance: La distancia total recorrida al interior de vehículos, en metros.

&nbsp;	swimDistance: La distancia total nadando por el agua, en metros.



Clasificaciones (Sistemas de Puntuación Externos del Juego)

&nbsp;	killPlace: El ranking interno de esa partida basándose únicamente en quién mató más.

&nbsp;	killPoints: Un ranking externo para el jugador basado en asesinatos (similar a un sistema Elo competitivo).

&nbsp;	rankPoints: Una clasificación general tipo Elo del jugador dentro del juego.

&nbsp;	winPoints: La cantidad de puntos de victoria previos acumulados por este jugador.



La Variable Objetivo (y)	

&nbsp;	winPlacePerc: Este es el porcentaje o percentil de colocación en el que terminó el jugador. Esta es la columna continua que tu algoritmo intentará adivinar, donde 1 corresponde al absoluto ganador (primer lugar) y 0 al primer muerto de la partida.





----------------------------------------------------------------------------------------------------------------------------------------------------------------



Las Columnas (n características): Son las variables o atributos (kills, daño, distancia caminada, etc.).

Las Filas (m ejemplos): Es un registro individual. En este caso, cada fila es la partida de un solo jugador

&nbsp;	

Id (Jugador)	matchId (Partida)	kills	damageDealt	headshotKills	heals	walkDistance	weaponsAcquired	...	winPlacePerc (Y)

7f96b2f8	4d1bb11	0	25.93	0	0	244.8	1	...	0.4444	244.80		1		...	0.4444

eef90569	684d565	1	150.2	0	1	1434	5	...	0.64	1434.00		5		...	0.6400

1eaf90ac	6a4a42c	4	450.5	2	4	2560.2	6	...	0.9565	2560.20		6		...	0.9565

4616d365	19e9064	0	0	0	0	12.5	0	...	0	12.50		0		...	0.0000





* Fila 1: Este jugador no mató a nadie (kills=0), hizo muy poco daño (25.93), caminó poco (244m) y agarró solo un arma. Como resultado, quedó casi a la mitad de la tabla (winPlacePerc = 0.4444 o 44%).



* Fila 3: Este es un jugador "Tryhard". Mató a 4 (kills=4), hizo muchísimo daño (450.5), dio 2 tiros a la cabeza, se curó 4 veces y caminó más de 2 kilómetros y medio (2560m). Por lo tanto, su posición final fue excelente, casi ganando la partida (winPlacePerc = 0.9565 o 95%).



* Fila 4: Probablemente alguien que cayó del avión y lo mataron al instante o se desconectó. Todo en cero, no caminó nada. Su posición final es el último lugar absoluto (winPlacePerc = 0.0000).





Cuando le pases esto a tu Ecuación de la Normal o a tu Descenso de Gradiente, la matemática va a analizar estas millones de filas simultáneamente para descubrir los "patrones ocultos". Por ejemplo, el modelo podría descubrir matemáticamente que walkDistance (caminar mucho) te asegura un mejor top final que volverte loco buscando kills.



-----------------------------------------------------------------------------------------------------------------------------------------------------------------

**¿Qué es la "Telemetría"?** Es simplemente la palabra técnica para referirse al "rastreo de datos". Cada vez que un jugador da un paso, recoge un arma o dispara, el servidor del juego guarda ese dato. A ese registro automático de acciones se le llama telemetría.



**¿Qué son "100 agentes por sesión"?** En Inteligencia Artificial, a los jugadores controlados por humanos o bots se les llama "agentes". Y la "sesión" es simplemente una partida. Entonces, significa "100 jugadores por partida".



**¿Cómo llegamos a "millones de ejemplos (filas)"?** ¡Aquí está el truco! El dataset no es de una sola partida. El dataset recopila los resultados finales de miles y miles de partidas distintas.



* Piensa que en 1 sola partida hay 100 jugadores. Cuando esa partida termina, el juego genera 100 filas de datos (una fila con las estadísticas finales de cada jugador).



* Si el dataset juntó los datos de 1.000 partidas, entonces tienes 100.000 filas.



* Este dataset de PUBG en Kaggle recopiló decenas de miles de partidas, por eso tiene millones de filas en total. Cada fila es el resumen de lo que hizo un jugador en una partida específica.



----------

**¿Qué significa una "escala continua de 0 a 1"?**

Es una excelente pregunta y es clave para que entiendas tu variable objetivo (y).En lugar de decir "quedaste en el puesto 1" o "quedaste en el puesto 87" (lo cual son números enteros), el dataset convierte tu posición final en un porcentaje o percentil, expresado en decimales. 



A esto se le llama una escala continua.



Imagina una partida con 100 jugadores:

&nbsp;	

&nbsp;	**0.0 (El peor):** Este es el jugador que cayó del avión y fue el primero en morir. Sobrevivió al 0% de los jugadores.

&nbsp;	**0.5 (La mitad):** Este jugador murió exactamente a la mitad de la partida. Quedó en el top 50.

&nbsp;	**0.9 (Top 10):** Este jugador llegó casi al final, sobreviviendo más que el 90% de la sala.

&nbsp;	**1.0 (El ganador):** El único jugador que quedó vivo ("Winner Winner Chicken Dinner"). Sobrevivió al 100% de sus oponentes.



**¿Por qué se hace así en Machine Learning?**

&nbsp;	Porque a los algoritmos de regresión multivariable (como el que vas a programar) les resulta matemáticamente mucho más fácil y preciso predecir un decimal continuo (ej. 0.83) que intentar adivinar un número de ranking exacto e inflexible. De hecho, al tener los datos de esta forma, ya están prácticamente normalizados en esa columna.









----------------------------

NOTA:



El modelo de regresión multivariable que vamos a programar para este laboratorio es universal para cualquier juego competitivo, porque la matemática detrás del algoritmo es exactamente la misma.



La única diferencia es que cambiarían las "columnas". Por ejemplo:



* En Fortnite: Tu modelo tendría las mismas columnas de daño y distancia, pero agregarías columnas como estructuras\_construidas o materiales\_recolectados.



* En Free Fire: Agregarías columnas sobre el uso\_de\_habilidades\_activas o mascotas.



* En Brawl Stars: En lugar de 100 jugadores, predecirías el resultado de una partida 3v3 basándote en el brawler\_elegido, gemas\_recolectadas o daño\_a\_la\_caja.





El algoritmo aprendería de la misma forma: analizando qué acciones tienen más "peso" matemático para asegurar la victoria.



----------------------------

&nbsp;	IMPORTANTE TALVES PARA EXPONER



**¿Por qué no hay datasets iguales de Fortnite o Free Fire?**

Es una excelente pregunta. La respuesta corta es: el monopolio de los datos.



**El secreto industrial:** Empresas como Epic Games (Fortnite), Garena (Free Fire) o Supercell (Brawl Stars, Clash Royale) protegen su telemetría como si fuera oro. No hacen públicas estas bases de datos masivas porque sus competidores podrían analizarlas para copiar sus fórmulas de emparejamiento (matchmaking) o retención de jugadores.



**La rareza del dataset de PUBG:** El dataset que elegiste es una verdadera joya ("un unicornio" en ciencia de datos). Existe únicamente porque en 2018 los desarrolladores de PUBG Corporation se asociaron con Kaggle para hacer un concurso mundial. Liberaron esta base de datos oficial y le pagaron miles de dólares a los programadores que lograran hacer el mejor modelo de predicción. ¡Por eso es tan masivo, limpio y perfecto para tu universidad!



**Lo que encuentras de otros juegos:** Si buscas de Fortnite o Free Fire, vas a encontrar datasets muy pequeños (de 1,000 o 2,000 filas) hechos por fans que copiaron los datos a mano de páginas de estadísticas. Casi ninguno cumple con la regla de tu docente de "más de 20.000 datos y más de 20 características".



