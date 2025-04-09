Режим генерации скриптов задаётся перечислением DbScriptGenerationMode:

1) `DbScriptGenerationMode.CREATE_AND_DROP` - полная генерация скриптов инициализации и обновления;
2) `DbScriptGenerationModeCREATE_ONLY` - полня генерация скриптов инициализации. Скрипты обновления
генериуются без операторов удаления столбцов.
3) `DbScriptGenerationMode.DISABLED` - скрипты инициализации и обновления не генерируются.

Значение по умолчанию: CREATE_AND_DROP.