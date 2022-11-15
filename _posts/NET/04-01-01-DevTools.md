---
title: Dev Tools
description: Basic Dev tools
categories:
- NET
tags:
- NAS
- Network
permalink: /devtools/
---



# Team City

1. https://www.postgresql.org/
- sql:   - moth - p: 5432
2. TC
- server p: 8111
  - System Account
  - User Account
3. Open:
- http://localhost:8111
  - postgress
  - zpisac z admina dane
4. run: pgAdnim :
  - pass: moth
  - create new database
5. localhost::8111
 - postgres
 - login: --- / hasło: ---
6. http://localhost:8111/agents/overview

jak nie działa to:
7.  gpedit.msc  - jak nie ma to: skrypt z katalogu w razie windows home
8. Agent instalesr
 - zainstalowac na swoim katalogu gdzie beda pliki sie budowac
 - http://localhost:8111/agent/1
 - http://localhost:8111/admin/admin.html?item=projects

Manual create project
 - creare  
 - zmieny hostów .... to co na screenach
10. Instal Visual Elements.....
 - https://app.vsaex.visualstudio.com/profile/create?mkt=en-us&campaign=o~msft~vscom~signin
 - https://my.visualstudio.com/Downloads
W instalerze:
 - .NET .... nugets

=============

PROJECT BUILD

# Atom

Sync git hub :
- `Shift` + `P`: GitHub:Clone

# Github

# Perforce

https://forums.perforce.com/index.php?/topic/3330-perforce-on-synology-and-unreal-engine-4/

...

Install
- helix pobrany:  p4d (dla linuxa 64) pobiera zzipowane archiwum z plikami
- `p4_start.sh` - skrypt do uruchamiania / instalacji
- Instalation script run:
   - ssh & `cd` to p4 catalog
   - `./p4_start.sh start`

Restart
- Restart
   - `cd /volume1/xxx/data/p4`
   - `./p4_start.sh start`  
- Check if running
      - `ps` wyswietla procesy sytemowe
- Kill process
      - `kill -9 xxxPIDxxx` < # 9 = kod sygnałyu SIG TEMINATE   

```bash

#!/bin/sh
#
#
# Startup/shutdown script for Perforce
#

# Source function library. this is where ‘daemon’ comes from
#. /etc/init.d/functions

prog="Perforce Server"

p4d_bin=/volume1/xxx/p4d
p4_bin=/volume1/xxx/p4
p4user=p4admin
p4authserver=p4authserver:1678
p4root=/volume1/data/p4
p4journal=/volume1/xxx/journal
p4port=1678
p4log=/volume1/xxx/log
p4loglevel=3

export PATH=/volume1/xxx/:$PATH
export P4PORT=1678
export P4USER=p4admin

start () {

# start

#If you wish to use a perforce auth server add this into the below command line.
# -a $p4authserver

# /bin/su $p4user -c “$p4d_bin -r $p4root -J $p4journal -p $p4port -L $p4log -v server=$p4loglevel -d” &>/dev/null
$p4d_bin -C1 -r $p4root -J $p4journal -p $p4port -L $p4log -v server=$p4loglevel -d
}

stop () {
# stop
echo Stopping $prog:
$p4_bin -p $p4port admin stop
}

restart() {
stop
start
}

case $1 in
start)
start
;;
stop)
stop
;;
restart)
restart
;;
*)

echo "Usage: ./p4_start.sh {start|stop|restart}"
exit 3
esac

exit $RETVAL
```








===================================================
==================================================

Errors:   
- If problems during instalation add variable: `export P4PORT=1666` (w konsoli nie wie z czym sie połaczyc bo zmienne typu $P4 port sie nie zapisują)
- test P4: reconcile /

ustawic 1 admina na p4Admin
konta dla programistów i nieprog

new file > depot - type stream
new group - mandala  

new users
- mr.robot
- deveolper
- admin

consola:
p4 set P4PORT=connect.mothdev:1678
P4 set P4USER = admin
p4 set P4PASSWD=123
p4 set


- mapa:
p4 typemap

l - log - musisz wyczekoawc zeby edytowac
w - do wszystk
sw - bes hostroii

ze
p4 configure set  reconcile - sm.status.matchlines=0


=========================

new workspace

Stream new stream  type r virtual - used to narrow space
from mandala
location: //mandala/mandalacode
add to ignore


advandced add to ignore
\
2 stream tez wirtual dla content
jurnal - plik w p4 ktory puchnie mozna go usuwac poprostu
