## Harding checklist linux 
--Доступ по SSH
Домашние пользователи:
Домашние пользователи на самом деле не используют ssh, динамические IP-адреса и конфигурации маршрутизатора NAT сделали альтернативы с обратным подключением, такие как TeamViewer, более привлекательными. Когда служба не используется, порт должен быть закрыт как путем отключения или удаления службы, так и путем применения ограничительных правил брандмауэра.

--Серверы:
В отличие от работников внутренних пользователей, обращающихся к разным серверам, сетевые администраторы часто используют ssh/sftp. Если необходимо включить службу ssh, можно принять следующие меры:

Отключите root - доступ через SSH.
Отключите вход по паролю.
Измените порт SSH.
