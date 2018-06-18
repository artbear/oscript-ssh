# Oscript SSH client 

## SSH клиент для oscript

### Пример использования для ssh 

```bsl
#Использовать clientSSH
    
КлиентSSH = Новый КлиентSSH("127.0.0.1", 22, "user", "password");
Соединение = КлиентSSH.ПолучитьСоединение();
Результат = Соединение.ВыполнитьКоманду("echo 123");   
    
Соединение.Разорвать();

```

### Пример использования для конфигуратора в режиме Агента 

Запустить конфигуратор в режиме агента:  
`
1cv8.exe DESIGNER /F"<ПутьКБазе>" /AgentMode /Visible /AgentSSHHostKeyAuto /AgentBaseDir "<ПутьКПапкеВыгрузки>"
`


```bsl
#Использовать clientSSH

КлиентSSH = Новый КлиентSSH("127.0.0.1", 1543, "admin", "");
Поток = КлиентSSH.ПолучитьПоток();
// Обязательно иначе вешается
Результат = Поток.ЗаписатьВПоток("options set --show-prompt=no --output-format=json");
Результат = Поток.ЗаписатьВПоток("common connect-ib");
Результат = Поток.ЗаписатьВПоток("config dump-config-to-files --dir .");
Результат = Поток.ЗаписатьВПоток("common disconnect-ib");

Поток.Разорвать();

```

## Известные проблемы:
* Вешается поток если не передать:  
 `Поток.ЗаписатьВПоток("options set --show-prompt=no --output-format=json");`  
 * В папке выгрузки создается подпапка с именем пользователя
 