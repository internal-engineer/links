# Дополнительные материалы к [этому видео](#)
[Инструкция по установки Node-RED](https://www.youtube.com/watch?v=IReCHprxwQ8) и некоторых других сервисов  
[Урок по базовым нодам Node-RED](https://www.youtube.com/watch?v=ucTUK3zNX1M)

Ссылки на официальную документацию Node-RED:

 - [Про контекст](https://nodered.org/docs/user-guide/context)
 - [Как найти settings.js](https://nodered.org/docs/user-guide/runtime/settings-file)

Настройка дающая возможность выбора расположения контекста:

    contextStorage: {
       default: "memoryOnly",
       memoryOnly: { module: 'memory' },
       file: { module: 'localfilesystem' }
    },

Тут можно скачать [код примера](https://github.com/internal-engineer/links/blob/main/contextStorage_and_sqlite.json) из видео.  
Ноды которые нужно доустановить:

 - [node-red-node-sqlite](https://flows.nodered.org/node/node-red-node-sqlite)
 - [node-red-contrib-cron-plus](https://flows.nodered.org/node/node-red-contrib-cron-plus)
