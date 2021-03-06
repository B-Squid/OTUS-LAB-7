/bin/sh

После загрузки выполняем следующие команды(в задании предполагается видимо смена пароля):
```
/usr/sbin/load_policy -i - загрузка политик SELinux. Если этого не сделать, то потребуется дополнительная 
перезагрузка с восстановлением контекста безопасности. 
Либо выполнить команды restorecon /etc/shadow и setenforce 1. restorecon - восстановить заданный по 
умолчанию контекст безопасности SELinux для файла(файлов).
mount -o remount,rw / - перемонтируем корень в режиме чтения/записи
passwd root - смена пароля пользователя root
mount -o remount,ro / - пермонтируем ФС в режиме чтения, что бы достоверно применить все изменения в открытых 
файлах, и получить "чистую" ФС при следующем запуске
exec /usr/sbin/init 6 - перезагрузка
```
Загрузка указанного исполняемого файла вместо /sbin/init, происходит сразу же после загрузки ядра. 
Соотвественно не будут загружены службы (sshd например), нельзя будет презапустить машину через 
стандартные команды. "Настоящая" ФС доступна. Наименее предпочтительный способ, в силу сниженной функциональности.

============================

rd.break 
При выполнении загрузки с этим параметром мы попадаем в emergency shell. 

После загрузки выполним следующие команды:
```
mount -o remount,rw /sysroot - -//-
chroot /sysroot - это вызов новой оболочки таким образом, что /sysroot становится / . Теперь /etc/passwd 
становится "настоящим". Перед тем как выполнять редактирование /etc/passwd мы должны сменить файловую систему, 
иначе все это не будет иметь никакого смысла (мы же находимся внутри initramfs).
passwd root - -//-
touch /.autorelabel - в случае активного SELinux запуск триггера на autorelabeling(восстановление контекста 
безопасности) всей ФС, может занять значительное время.
exit - выход из chroot-оболочки
exit - выход из emergency shell, что вызовет автоматическую перезагрузку(в силу отработки boot-скриптов, 
отслеживающих закрытие emergency shell).
```
Мы попадаем в оболочку в конце обработки initramfs, init доступен. В отличие от первого способа настоящая 
корневая ФС не монтируется в /, ядро располагает только initramfs, с соотвествующими утилитами. На данном 
этапе настоящая ФС смонтирована в /sysroot  (далее должен быть pivot_root).

=============================

/sysroot/bin/sh

При загрузке мы попадаем в однопользовательский режим, сразу в "настоящую" ФС. Остальное аналогично.
