#### Примеры запросов к API для работы почтовым сервером.
Описание API методов работы с почтовым сервером Р7.<br>
Можно отправлять POST-запросы с данными.<br> 
Описание методов REST API.<br>

**Создание почтового ящика.**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"email":"test@domain.ru","password":"mail_password"}&apos; https://admin.domain.ru/apimail/create_user --user admin:PassworD
```
*Описание:*
```bash
email — почтовый ящик для создания пользователя.
password — пароль для пользователя почтового ящика.
https://admin.domain.ru/apimail/create_user — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```
*Пример:*
```bash
#!/bin/bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer eyJhbGciOiJIUzI1NiI
.eyJ1c2VyX2VtYWlsIjoic3VwZXJhZG1pbkBOb25lIiwic2NvcGVzIjpbImdlbmxr0TcHZ2N24VtCu8werf4rdfre
VyYXRlX3Rva2VuIiwiYXNzaWduX3Njb3BlIiwicmV2b2tlX3Njb3BlIiwibGlzdF9hZG1pbnMiLCJjcmVhdGVfdXN
lciIsImNoYW5nZV9wYXNzd29yZCIsImNoYW5nZV9lbWFpbCIsImRlbGV0ZV91c2VyIiwiY3JlYXRlX2FsaWFzIiwi
Y3JlYXRlX2FsaWFzX211bHR5IiwiY2hhbmdlX2FsaWFzIiwiZGVsZXRlX2FsaWFzIiwiY3JlYXRlX2RvbWFpbiIsI
mRlbGV0ZV9kb21haW4iLCJjaGVja19lbWFpbCIsIm1haWxib3hfc2l6ZSIsInNldF9xdW90YSIsImNyZWF0ZV9zaG
FyZWRfbWFpbGJveCIsImFkZF9hY2wiLCJyZW1vdmVfYWNsIiwiZ2V0X2FjbCIsImdldF9saW1pdHMiLCJzZXRfc2V
uZF9saW1pdCIsImRlbGV0ZV9saW1pdCIsIm1vZGlmeV9saXN0IiwibWFpbF9xdWV1ZSJdfQ.3C3E5gnR7Xseq4RoN" -d '{"old_email":"test1@ald.vit.lan","new_email":"newtest@ald.vit.lan"}' https://admin.ald.vit.lan/apimail/change_email --user admin:passwd
```

**Изменение пароля почтового ящика.**

```bash
curl -X POST -H "Content-Type: application/json" -d -H "jwt-auth: Bearer <jwt-token>” &apos;{"email":"test@domain.ru","password":"new_password"}&apos; https://admin.domain.ru/apimail/change_password --user admin:PassworD
```
*Описание:*
```bash
email — почтовый ящик, для которого изменяется пароль.
password — новый пароль для пользователя почтового ящика.
https://admin.domain.ru/apimail/change_password — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Изменение имени почтового ящика (с копированием директории с почтовыми данными).**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"old_email":"test@domain.ru","new_email":"test2@domain.ru"}&apos; https://admin.domain.ru/apimail/change_email --user admin:PassworD
```
*Описание:*
```bash
old_email — текущий почтовый ящик.
new_email — новое имя почтового ящика.
https://admin.domain.ru/apimail/change_email — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Удаление почтового ящика (с удалением данных почты).**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"email":"test@domain.ru"}&apos; https://admin.domain.ru/apimail/delete_user --user admin:PassworD
```
*Описание:*
```bash
email — почтовый ящик для удаления.
https://admin.domain.ru/apimail/delete_user — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Создание нового алиаса.**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"alias":"news@domain.ru","email":"user@domain.ru"}&apos; https://admin.domain.ru/apimail/create_alias --user admin:PassworD
```
*Описание:*
```bash
alias — адрес алиаса (например, news@domain.ru).
email — основной почтовый ящик, на который будет перенаправляться почта.
https://admin.domain.ru/apimail/create_alias — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Создание нового домена (c генерацией ключа opendkim).**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"name":"new-domain.ru"}&apos; https://admin.domain.ru/apimail/create_domain --user admin:PassworD
```
*Описание:*
```bash
name — имя нового домена (например, new-domain.ru).
https://admin.domain.ru/apimail/create_domain — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Получение DKIM записи домена (если необходимо добавить в глобальный DNS, для повышения доверия к домену).**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"domain":"new-domain.ru"}&apos; https://admin.domain.ru/apimail/get_dkim --user admin:PassworD
```
*Описание:*
```bash
domain — имя домена (например, new-domain.ru).
https://admin.domain.ru/apimail/get_dkim — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```
**Удаление домена (c удалением данных opendkim).**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"name":"domain.ru"}&apos; https://admin.domain.ru/apimail/delete_domain --user admin:PassworD
```
*Описание:*
```bash
name — имя домена для удаления.
https://admin.domain.ru/apimail/delete_domain — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Создание алиаса с несколькими получателями.**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"source":"news_users@domain.ru","destinations":"user3@domain.ru,user4@domain.ru"}&apos; https://admin.domain.ru/apimail/create_alias_multy --user admin:PassworD
```
*Описание:*
```bash
source — адрес алиаса (например, news_users@domain.ru).
destinations — список получателей, разделенных запятой (например, user3@domain.ru,user4@domain.ru).
https://admin.domain.ru/apimail/create_alias_multy — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Изменение алиаса (для одного получателя).**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"source":"news@domain.ru","destinations":"news5@domain.ru"}&apos; 
https://admin.domain.ru/apimail/change_alias --user admin:PassworD
```
*Описание:*
```bash
source — текущий адрес алиаса.
destinations — новый получатель для алиаса.
https://admin.domain.ru/apimail/change_alias — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Удаление алиаса.**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"alias":"news@domain.ru"}&apos; https://admin.domain.ru/apimail/delete_alias --user admin:PassworD
```
*Описание:*
```bash
alias — адрес алиаса для удаления.
https://admin.domain.ru/apimail/delete_alias — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Проверка наличия почтового ящика.**
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"email":"user@domain.ru"}&apos; https://admin.domain.ru/apimail/check_email --user admin:PassworD
```
*Описание:*
```bash
email — почтовый ящик для проверки.
https://admin.domain.ru/apimail/check_email — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Получение информации по объёму почтового ящика.**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"email":"user@domain.ru"}&apos; https://admin.domain.ru/apimail/mailbox_size --user admin:PassworD
```
*Описание:*
```bash
email — почтовый ящик для получения информации.
https://admin.domain.ru/apimail/mailbox_size — адрес вызова API.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
```

**Установка квоты для почтового ящика.**

Метод позволяет установить квоту (ограничение на объем хранилища) для указанного почтового ящика.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"email":"user@domain.ru","quota":1024}&apos; https://admin.domain.ru/apimail/set_quota --user admin:PassworD
```
*Описание:*
```bash
email — почтовый ящик, для которого устанавливается квота.
quota — квота в мегабайтах (MB). Должна быть положительным числом.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/set_quota
```

**Создание общего почтового ящика.**

Метод создает общий почтовый ящик и предоставляет доступ к нему указанному пользователю.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"from_user":"shared@domain.ru","to_user":"user@domain.ru","password":"shared_password"}&apos; https://admin.domain.ru/apimail/create_shared_mailbox --user admin:PassworD
```
*Описание:*
```bash
from_user — имя общего почтового ящика (например, shared@domain.ru).
to_user — пользователь, которому предоставляется доступ к общему ящику (опционально).
password — пароль для общего почтового ящика.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/create_shared_mailbox
```

**Добавление ACL для общего почтового ящика.**

Метод добавляет права доступа (ACL) для указанного пользователя к общему почтовому ящику.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"shared_mailbox":"shared@domain.ru","user":"user@domain.ru","rights":"read write"}&apos; https://admin.domain.ru/apimail/add_acl --user admin:PassworD
```
*Описание:*
```bash
shared_mailbox — имя общего почтового ящика.
user — пользователь, которому предоставляются права.
rights — права доступа (например, read, write).
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/add_acl
```

**Удаление ACL для общего почтового ящика.**

Метод удаляет права доступа (ACL) для указанного пользователя к общему почтовому ящику.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"shared_mailbox":"shared@domain.ru","user":"user@domain.ru","rights":"read write"}&apos; https://admin.domain.ru/apimail/remove_acl --user admin:PassworD
```
*Описание:*
```bash
shared_mailbox — имя общего почтового ящика.
user — пользователь, у которого удаляются права.
rights — права доступа, которые необходимо удалить (например, read, write).
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/remove_acl
```

**Получение ACL для общего почтового ящика.**

Метод возвращает права доступа (ACL) для указанного пользователя к общему почтовому ящику.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"shared_mailbox":"shared@domain.ru","user":"user@domain.ru"}&apos; https://admin.domain.ru/apimail/get_acl --user admin:PassworD
```
*Описание:*
```bash
shared_mailbox — имя общего почтового ящика.
user — пользователь, для которого запрашиваются права.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/get_acl
```

**Получение очереди почтового сервера.**

Метод возвращает состояние очереди почтового сервера.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -H "Authorization: Bearer <твой_JWT_токен>" https://admin.domain.ru/apimail/mail_queue --user admin:PassworD
```
*Описание:*
```bash
user — пользователь, для которого запрашиваются права.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/mail_queue
```

**Получение списка лимитов на отправку почты.**

Метод возвращает лимиты установленные на ящик, домен, общие.
```bash
curl -X POST -H "Content-Type: application/json"  -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"identifier":"mailbox@domain.ru","id_type":"email","limit_type":"send"}&apos; https://admin.domain.ru/apimail/get_limits --user admin:PassworD
```
*Описание:*
```bash
identifier — имя почтового ящика, домен.
id_type – указываем для чего правила ("email", "domain", "group", "server")
limit_type – указываем тип лимита ("send", "rcpt")
user — пользователь, для которого запрашиваются права.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/get_limits
```

**Установка лимитов на отправку почту.**

Метод возвращает лимиты установленные на ящик, домен, общие.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"identifier":"mailbox@domain.ru","id_type":"email","limit": 1,"period":"hour","limit_type":"send"}&apos; https://admin.domain.ru/apimail/set_send_limit --user admin:PassworD
```
*Описание:*
```bash
identifier — имя почтового ящика, домен.
id_type – указываем для чего правила ("email", "domain", "group", "server")
limit – количество писем,
period – указывается в течение какого периода ("hour", "day", "week")
limit_type – указываем тип лимита ("send", "rcpt")
user — пользователь, для которого запрашиваются права.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API: https://admin.domain.ru/apimail/set_send_limit
```

**Удаление лимитов на отправку почты.**

Метод возвращает лимиты установленные на ящик, домен, общие.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{"identifier":"mailbox@domain.ru","id_type":"email","limit_type":"send"}&apos; https://admin.domain.ru/apimail/delete_limit --user admin:PassworD
```
*Описание:*
```bash
identifier — имя почтового ящика, домен.
id_type – указываем для чего правила ("email", "domain", "group", "server")
limit_type – указываем тип лимита ("send", "rcpt")
user — пользователь, для которого запрашиваются права.
admin:PassworD  - пользователь и пароль созданные в пункте 11.2
Адрес вызова API:
 https://admin.domain.ru/apimail/delete_limit
```

**Управление черным или белым списком.**

Метод добавляет почтовый адрес, домен или ip-адрес в черный или белый список список.<br>
Добавление в черный список.
```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{
    "action": "add",
    "entry": "spam@example.ru",
    "list_type": "blacklist"
}&apos; https://admin.domain.ru/apimail/modify_list --user admin:PassworD
```

**Удаление из белого списка.**

```bash
curl -X POST -H "Content-Type: application/json" -H "jwt-auth: Bearer <jwt-token>” -d &apos;{
    "action": "remove",
    "entry": "trusted@example.ru",
    "list_type": "whitelist"
}&apos; https://admin.domain.ru/apimail/modify_list --user admin:PassworD
```
*Описание:*
```bash
action — add (добавить) или remove (удалить).
entry — email, домен или IP-адрес.
ist_type — blacklist (черный список) или whitelist (белый список).
Адрес вызова API: https://admin.domain.ru/apimail/modify_list
```

**Управление правами пользователей (JWT-аутентификация).**

Выдача токена.
```bash
curl -X POST -H "Content-Type: application/json" -d &apos;{
    "email": "admin@domain.ru"
}&apos; https://admin.domain.ru/apimail/generate_token --user admin:PassworD
```
*Описание:*
```bash
email — email пользователя, для которого создается JWT-токен.
```

**Назначение прав пользователю.**

```bash
curl -X POST -H "Content-Type: application/json" -d &apos;{
    "email": "user@domain.ru",
    "scope": "create_user"
}&apos; https://admin.domain.ru/apimail/assign_scope --user admin:PassworD
```
*Описание:*
```bash
email — email пользователя.
scope — назначаемое право (например, create_user, delete_user).
```

**Удаление прав у пользователя.**

```bash
curl -X POST -H "Content-Type: application/json" -d &apos;{
    "email": "user@domain.ru",
    "scope": "create_user"
}&apos; https://admin.domain.ru/apimail/revoke_scope --user admin:PassworD
```
*Описание:*
```bash
email — email пользователя.
scope — назначаемое право (например, create_user, delete_user).	
```

**Получение списка администраторов для управления правами:**

    • Запрашивает список пользователей, у которых есть права администратора.
    • Возвращает массив email-адресов.
```bash
curl -X POST -H "Content-Type: application/json" -d &apos;{
    "email": "user@domain.ru",
    "scope": "create_user"
}&apos; https://admin.domain.ru/apimail/revoke_scope --user admin:PassworD
``` 

