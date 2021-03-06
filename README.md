

## Содержание
1. Введение
2. Основы усиления безопасности Linux
 - Доступ по SSH
 - Iptables
 - Система обнаружения вторжений (IDS)
 - Безопасность BIOS
 - Шифрование жесткого диска
 - Шифрование жесткого диска
 - Обновление системы
 - VPN (виртуальная частная сеть)
 - Включить SELinux (Linux с улучшенной безопасностью)
3. Общие практики
4. Вопросы
5. Список литературы
## Введение
Защита вашего сервера Linux важна для защиты ваших данных, интеллектуальной от взломщиков (хакеров).
В этом руководстве перечислены начальные меры безопасности как для пользователей настольных компьютеров, так и для системных администраторов, управляющих серверами. В руководстве указывается, когда рекомендация предназначена для домашних или профессиональных пользователей. 

## 1) Доступ по SSH

 Домашние пользователи:
Домашние пользователи на самом деле не используют ssh, динамические IP-адреса и конфигурации маршрутизатора NAT сделали альтернативы с обратным подключением, такие как TeamViewer, более привлекательными. Когда служба не используется, порт должен быть закрыт как путем отключения или удаления службы, так и путем применения ограничительных правил брандмауэра.

 Серверы:
В отличие от работников внутренних пользователей, обращающихся к разным серверам, сетевые администраторы часто используют ssh/sftp. Если необходимо включить службу ssh, можно принять следующие меры:
* Отключите root - доступ через SSH.
* Отключите вход по паролю.
* Измените порт SSH.

 
## 2) Iptables
**Iptables -это интерфейс для управления netfilter для определения правил брандмауэра. Домашние пользователи могут иметь тенденцию к UFW (несложный брандмауэр) который является интерфейсом для iptables, чтобы упростить создание правил брандмауэра**. Независимо от интерфейса дело в том, что сразу после установки брандмауэр является одним из первых изменений. 
В зависимости от потребностей вашего рабочего стола или сервера наиболее рекомендуемыми для обеспечения безопасности являются ограничительные политики, разрешающие только то, что вам нужно, и блокирующие все остальное. Iptables будут использоваться для перенаправления SSH-порта 22 на другой, для блокировки ненужных портов, фильтрации сервисов и установки правил для известных атак.
## 3) Система обнаружения вторжений (IDS)
Из-за больших ресурсов, которые они требуют IDS не используются домашними пользователями, но они являются обязательными на серверах, подверженных атакам. **IDS выводит безопасность на новый уровень, позволяя анализировать пакеты. Наиболее известными идентификаторами являются Snort и OSSEC. IDS анализирует трафик по сети в поисках вредоносных пакетов или аномалий, это инструмент мониторинга сети, ориентированный на инциденты безопасности**. Для получения инструкций по установке и настройке для большинства 2 популярных решений IDS проверьте: Настройка Snort IDS и создание правил
## 4) Безопасность BIOS
Руткиты, вредоносные программы и серверные BIOS с удаленным доступом представляют собой дополнительные уязвимости для серверов и настольных компьютеров. BIOS можно взломать с помощью кода, выполняемого из ОС, или через каналы обновления, чтобы получить несанкционированный доступ или забыть информацию, такую как резервные копии безопасности.
**Обновляйте механизмы обновления BIOS. Включите защиту целостности BIOS.**
## 5) Шифрование жесткого диска
Эта мера более актуальна для пользователей настольных компьютеров, которые могут потерять свой компьютер или стать жертвой кражи, она особенно полезна для пользователей ноутбуков. **Сегодня почти каждая ОС поддерживает шифрование дисков и разделов, такие дистрибутивы, как Debian, позволяют шифровать жесткий диск в процессе установки**.
## 6) Обновление системы
Как пользователи настольных компьютеров, так и сисадмин должны поддерживать систему в актуальном состоянии, чтобы предотвратить несанкционированный доступ или выполнение уязвимых версий. В дополнение к использованию диспетчера пакетов ОС для проверки наличия доступных обновлений запуск сканирования уязвимостей может помочь обнаружить уязвимое программное обеспечение, которое не было обновлено в официальных репозиториях, или уязвимый код, который необходимо переписать.
## 7) VPN (виртуальная частная сеть)
Интернет-пользователи должны знать, что интернет-провайдеры контролируют весь свой трафик, и единственный способ позволить себе это-использовать VPN-сервис. Интернет-провайдер может отслеживать трафик на VPN-сервер, но не от VPN до пунктов назначения. 
## 8) Включить SELinux (Linux с улучшенной безопасностью)
**SELinux - это набор модификаций ядра Linux, ориентированных на управление аспектами безопасности, связанными с политиками безопасности**, путем добавления MAC (Mechanism Access Control), RBAC (Role Based Access Control), MLS (Multi Level Security) и Multi Category Security (MCS). Когда SELinux включен, приложение может получить доступ только к необходимым ресурсам, указанным в политике безопасности приложения. Доступ к портам, процессам, файлам и каталогам контролируется с помощью правил, определенных в SELinux, которые разрешают или запрещают операции на основе политик безопасности. Ubuntu использует AppArmor в качестве альтернативы.
## Общие практики
Почти всегда сбои безопасности происходят из-за халатности пользователя. В дополнение ко всем пунктам перечисленным ранее выполните следующие действия:
Не используйте root без необходимости.
- Никогда не используйте X Windows или браузеры в качестве root.
- Используйте менеджеры паролей, такие как LastPass.
- Используйте только надежные и уникальные пароли.
- Попробуйте не устанавливать несвободные пакеты или пакеты, недоступные в официальных репозиториях.
- Отключите неиспользуемые модули.
- На серверах следует применять надежные пароли и запретить пользователям использовать старые пароли.
- Удалите неиспользуемое программное обеспечение.
- Не используйте одни и те же пароли для разных доступов.
- Измените все имена пользователей доступа по умолчанию.
- 
## Список литературы


1. [LinuxHint](<https://linuxhint.com/linux_security_hardening_checklist/>)
2. [UCD Linux Security Checklist.pdf](https://www.ucd.ie/t4cms/UCD%20Linux%20Security%20Checklist.pdf)
                                                                                                                                                   
