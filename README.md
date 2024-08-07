# Домашнее задание к занятию "`Репликация и масштабирование. Часть 2`" - `Клименко Олег`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Опишите основные преимущества использования масштабирования методами:

- активный master-сервер и пассивный репликационный slave-сервер;
- master-сервер и несколько slave-серверов;
- активный сервер со специальным механизмом репликации — distributed replicated block device (DRBD);
- SAN-кластер.

*Дайте ответ в свободной форме.*

- активный master-сервер и пассивный репликационный slave-сервер;

`При таком горизонтальном масштибировании у нас есть сервер для внесения, редактирования данных и копия сервера, которую можно использовать для чтения данных. Так как у нас всего два сервера то получаем простую настройку и минимальную нагрузку на сеть + безопасность данных, так как есть копия в виде slave-сервера`

- master-сервер и несколько slave-серверов;

`При таком масштабировании у нас больше серверов для чтения, следовательно запросов на чтение данных может быть больше, у нас больше копий данных, но возрастает и сложность настройки, идет больше нагрузка на сеть из-за синхронизации данных и общения между серверами.`

- активный сервер со специальным механизмом репликации — distributed replicated block device (DRBD);

`В данном случае имеем повышение отказоустройчивасти, так как на нескольких серверах можем иметь копии данных (БД) и в случае выхода из строя основного сервера, мы можем перемонтировать диск с базой данных на другом сервере и продолжить работать с ним как с основным сервером.`

- SAN-кластер.

`При использовании SAN-кластер решения получаем повышение отказоустойчивости и производительности, так как в системе должны быть избытычные (дублирующие) узлы, так же такую систему хранения данных проще обслужить или обновить на уровне железа, но данное решение будет отличатся более сложной настройкой и дороговизной.`

---

### Задание 2

Разработайте план для выполнения горизонтального и вертикального шардинга базы данных. База данных состоит из трёх таблиц:

- пользователи,
- книги,
- магазины (столбцы произвольно).

Опишите принципы построения системы и их разграничение или разбивку между базами данных.

*Пришлите блоксхему, где и что будет располагаться. Опишите, в каких режимах будут работать сервера.*

`Мы можем разбить общую БД на отдельные БД - DB Users, DB Books, DB Stores - это будет вертикальный шардинг, вторым шагом мы можем, например, большую БД с пользователями разбить на 2 сервера (горизонтальный шардинг) и на 1 сервере оставить id, имя, пароль, почту, адрес, телефон на другом сервере будем хранить историю заказов, посещения, любимые категории, избранные книги, доступ к книгам онлайн. Два сервера будут работать как master-сервера, для повышения производительности можно к первому серверу добавить slave-сервер.`

![](https://cdn.discordapp.com/attachments/1258766000980230166/1265232406168866908/4.png?ex=66a0c300&is=669f7180&hm=e5b73e683b3bd488cf0330d22bdcb76e18cb4c8bdf23cdbb21ebb3edd6712731&)

---
---











