# issabel Boss Secretary Senario
We want no one to take the bosses extension directly

We have two boss extension and one secretary

secretary and boss extensions :

> extension of secretary is : 101

> extension of boss1 is : 102

> extension of boss2 is : 103

- if you have 2 secretary extension or more put those to the Ring Group on web interface and use Ring Group Number here

1. open /etc/asterisk/globals_custom.conf and create global variables
``` asterisk
secretary=101
boss1=102
boss2=103
```
2. open /etc/asterisk/extensions_custom.conf create zarbinnetwork context and include it
``` asterisk
[from-internal-custom]
include => zarbinnetwork

[zarbinnetwork]
exten => ${boss1},1,GotoIf($[$[${CALLERID(num)}=${secretary}]|$[${CALLERID(num)}=${boss2}]]?from-internal-additional,${EXTEN},1:from-internal-additional,${secretary},1)
exten => ${boss2},1,GotoIf($[$[${CALLERID(num)}=${secretary}]|$[${CALLERID(num)}=${boss1}]]?from-internal-additional,${EXTEN},1:from-internal-additional,${secretary},1)
```
3. reload asterisk dialplan
``` asterisk
asterisk -r
reload
exit
```
