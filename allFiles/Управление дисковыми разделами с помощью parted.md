#linux 
Возможность деления дискового пространства на разделы позволяет создать
одну или несколько логически изолированных областей. На диске должен
иметься хотя бы один раздел. Количество разделов зависит только от ваших
потребностей и капризов. После создания разделов в каждый из них нужно
поместить файловую систему, и только тогда вы сможете использовать диск.
На одном диске может быть несколько разделов, и каждый раздел может иметь
свою файловую систему.


==🔴**Размонтирование разделов перед разбиением с помощью parted**==

Размонтировать раздел можно в диспетчере файлов с графическим интерфейсом
или воспользоваться командой **umount**. Ниже представлен пример размонтиро-
вания /dev/sdc2:
`$ sudo umount /dev/sdc2`

==🔴**Запуск parted в командном режиме**==
Если ввести команду parted без параметров, то она запустит интерактивную
оболочку parted . Для этого нужны привилегии root:
`$ sudo parted
`GNU Parted 3.2
`Using /dev/sda
`Welcome to GNU Parted! Type 'help' to view a list of commands.
`(parted)
Когда привычное приглашение к вводу сменится на (parted), это будет озна-
чать, что вы находитесь в интерактивной оболочке parted. Введите help, чтобы
получить список команд и их описания. Кроме того, можно получить справку
для отдельных команд parted, например help print. Введите quit, чтобы вый­
ти из parted. Большинство команд parted можно сократить до первой буквы,
например h и q.

Чтобы запустить parted как обычную команду, нужно передать ей все необ-
ходимые параметры, как в следующем примере, который выводит список всех
подключенных дисков:
`$ sudo parted /dev/sdb print devices
`/dev/sdb (2000GB)
`/dev/sda (4001GB)
`/dev/sdc (4010MB)
`/dev/sdd (15.7GB)
`/dev/sr0 (425MB)
Команда запустится, выполнит затребованное действие и вернется в обычную
командную оболочку.



==🔴**Создание разделов GPT на незагрузочном диске**==

Следующий пример демонстрирует разбиение USB-накопителя /dev/sdc , кото-
рый используется для хранения данных. Это не загрузочный диск с операцион-
ной системой. Перед запуском parted **обязательно размонтируйте устройство**.
Первый шаг — размонтировать устройство, и только потом можно приступать
к созданию новой таблицы разделов GPT:
`$ sudo umount /dev/sdc
`$ sudo parted /dev/sdc
`GNU Parted 3.2
`Using /dev/sdc
`Welcome to GNU Parted! Type 'help' to view a list of commands.
`(parted) mklabel gpt
`Warning: The existing disk label on /dev/sdc will be destroyed and all data on`
`this disk will be lost. Do you want to continue?`
`Yes/No? Yes`
`(parted) p`
`Model: General USB Flash Disk (scsi)`
`Disk /dev/sdc: 4010MB`
`Sector size (logical/physical): 512B/512B`
`Partition Table: gpt`
`Disk Flags:`
`Number`
 `Start`
 `End`
 `Size`
 `File system`
 `Name`
 `Flags`

Теперь можно создать новые разделы. Ниже приводится пример создания двух
разделов с одинаковыми размерами. Для каждого раздела нужно указать имя,
а также начало и конец:
`(parted) mkpart "images" ext4 1MB 2004MB`
`(parted) mkpart "audio files" xfs 2005MB 100%`

После этого проверьте получившийся результат и завершите сеанс работы
с parted:
`(parted) print`
`Model: General USB Flash Disk (scsi)`
`Disk /dev/sdc: 4010MB`
`Sector size (logical/physical): 512B/512B`
`Partition Table: gpt`
`Disk Flags:`
`Number  Start      End         Size       File system  Name      Flags`
`1             1049kB  2005MB 2004MB     ext4         images`
`2             2006MB 4009MB 2003MB     xfs         audio files`
`(parted) q`
`Information: You may need to update /etc/fstab.`

Если начало или конец окажется слишком близко к другому разделу, то parted
сообщит об ошибке. В следующем примере начало второго раздела совпадает
с концом первого:
`(parted) mkpart "images" ext4 2004MB 100%`
`Warning: You requested a partition from 2004MB to 4010MB (sectors`
`3914062..7831551).`
`The closest location we can manage is 2005MB to 4010MB (sectors`
`3915776..7831518).`
`Is this still acceptable to you?`
`Yes/No? Yes`
Чтобы исправить ошибку, можно 2004MB заменить на 2005MB.

==🔴**Удаление разделов**==

Запустите parted в интерактивном режиме для диска, на котором требуется
удалить разделы, и выведите таблицу разделов:
`$ sudo parted /dev/sdc`
`GNU Parted 3.2`
`Using /dev/sdc`
`Welcome to GNU Parted! Type 'help' to view a list of commands.`
`(parted) p`
`Model: General USB Flash Disk (scsi)`
`Disk /dev/sdc: 4010MB`
`Sector size (logical/physical): 512B/512B`
`Partition Table: msdos`
`Disk Flags:2`

| Number | Start  | End    | Size   | Type    | File system | Flags |
| ------ | ------ | ------ | ------ | ------- | ----------- | ----- |
| 1      | 1049kB | 2005MB | 2004MB | primary |             |       |
| 2      | 2005MB | 4010MB | 2005MB | primary |             |       |

Чтобы, например, удалить второй раздел, введите команду rm 2. Раздел будет
`немедленно удален без подтверждения. Затем снова введите команду p для`
`проверки:`
`(parted) rm 2`
`(parted) p`
`Model: General USB Flash Disk (scsi)`
`Disk /dev/sdc: 4010MB`
`Sector size (logical/physical): 512B/512B`
`Partition Table: msdos`
`Disk Flags:`

| Number | Start  | End    | Size   | Type    | File system | Flags |
| ------ | ------ | ------ | ------ | ------- | ----------- | ----- |
| 1      | 1049kB | 2005MB | 2004MB | primary |             |       |


==🔴**Восстановление удаленного раздела**==

Если вы случайно удалили новый пустой раздел, то нет смысла восстанавли-
вать его, просто создайте его заново. Если в разделе имелась файловая система
и данные, то приступить к восстановлению нужно немедленно. В интерактивной
оболочке parted выполните команду **rescue** и укажите начало и конец раздела.
Они могут быть приблизительными:
`(parted) rescue 2000MB 4010MB`
`searching for file systems... 40%`
 `(time left 00:01)Information: A ext4`
`primary partition was found at 2005MB -> 4010MB. Do you want to add it to the`
`partition table?`
`Yes/No/Cancel? Yes`
Оболочка parted не сообщает о результатах выполнения операции, поэтому вы-
ведите таблицу разделов, чтобы узнать, был ли восстановлен потерянный раздел:
`(parted) p`
`Model: General USB Flash Disk (scsi)`
`Disk /dev/sdc: 4010MB`
`Sector size (logical/physical): 512B/512B`
`Partition Table: gpt`
`Disk Flags:`

| Number | Start  | End    | Size   | Type    | File system | Flags |
| ------ | ------ | ------ | ------ | ------- | ----------- | ----- |
| 1      | 1049kB | 2005MB | 2004MB | primary |             |       |
| 2      | 2005MB | 4010MB | 2005MB | primary |             |       |

Чем дольше вы раздумываете, прежде чем приступить к восстановлению раз-
дела, тем ниже вероятность успешного восстановления, поскольку он может
быть случайно перезаписан. Если нужно отложить спасательные операции на
какое-то время, то спрячьте диск подальше в безопасное место.
Как всегда, не забывайте о резервном копировании.

==🔴**Увеличение размера раздела**==

Следующий пример демонстрирует, как увеличить размер раздела с файловой
системой в нем. Для этого нужно выполнить два шага: изменить размер раздела,
затем соответствующим образом изменить размер файловой системы. Каждая
файловая система имеет свой набор инструментов, и вы должны использовать
правильный инструмент для увеличения размера системы. В данном рецепте
мы изменим размер разделов Ext4, XFS, Btrfs и FAT16/32.
**Ext4, XFS и Btrfs можно увеличивать, не размонтируя их. Изменить размер
FAT16/32 можно, только если эта файловая система размонтирована**.
В конце раздела, который нужно увеличить, должно быть свободное место.
Откройте интерактивную оболочку parted на выбранном диске и найдите сво-
бодное место:

`$ sudo parted /dev/sdc`
`GNU Parted 3.2`
`Using /dev/sdc`
`Welcome to GNU Parted! Type 'help' to view a list of commands.`
`(parted) print free`
`Model: General USB Flash Disk (scsi)`
`Disk /dev/sdc: 4010MB`
`Sector size (logical/physical): 512B/512B`
`Partition Table: gpt`
`Disk Flags:`

| Number | Start  | End    | Size   | File system | Name  | Flags |
| ------ | ------ | ------ | ------ | ----------- | ----- | ----- |
| ...    |        |        |        |             |       |       |
|        | 1024MB | 2005MB | 981MB  | Free Space  |       |       |
| 2      | 2005MB | 3500MB | 1945MB | ext4        | audio |       |
|        | 3500MB | 4010MB | 510MB  | Free Space  |       |       |

В данном случае мы имеем 981 Мбайт свободного пространства перед разделом 2
и 510 Мбайт — после него. **Изменить можно только конечную точку раздела,
поэтому следующие примеры расширяют раздел 2, добавляя к нему 510 Мбайт
свободного места в конце**.
Сначала расширим раздел до новой конечной точки:
`(parted) resizepart 2 4010MB`
Вы не увидите сообщения об успешном выполнении, но если была допущена
ошибка, то сообщение об ошибке появится. Введите p, чтобы вывести таблицу
разделов и убедиться, что команда resizepart сделала то, что вы хотели.

Теперь нужно расширить файловую систему, приведя ее размер в соответ-
ствие с новым размером раздела, использовав для этого соответствующую
команду для данной файловой системы.

| Файловая система | Команда изменения размера                  |
| ---------------- | ------------------------------------------ |
| Ext4             | sudo resize2fs /dev/sdc2                   |
| XFS              | sudo xfs_growfs -d /dev/sdc2               |
| Btrfs            | sudo btrfs filesystem resize max /dev/sdc2 |
| FAT 16/32        | sudo fatresize -i /dev/sdc2                |



___
Раздел: [[Linux]]