ketika bekerja dengan state, copy state sebelumnya dengan menggunakan destructuring prev value. 
Karena array dan object pada javascript bersifat mutable.

Hal ini dapat menyebabkan bug, unpredicted behavior yang sulit ditrace.

Kecuali dalam fungsi reducer dari redux toolkit