# astra_mod_access
Доступ к Astra с ForkPlayer с генерацией токенов, все потоки  внутри плейлиста генерируются под пользователя и доступны только ему
Зайдя в админку astra каналам можно задавать groups (будет разбивка на категории в выходном m3u листе) и задать epg код в SERVICE / SERVICE NAME. Сам епг код  можно найти в ForkPlayer нажав на канале Меню \ ЕПГ код

В settings-http-auth-options можно указать ссылку на PROMO channel который будет показываться при отстутствии доступа
В settings-users можно добавлять пользователя с указанием даты окончания доступа и количества одновременных потоков, 
  уникальная ссылка на плейлист будет http://server:port/playlist.m3u8?auth=login:password
  ссылка будет работать в любом плеере и 
  не зависимо от настроек мода указаных ниже

whitelist_ip - список ip адресов которым будут доступны потоки напрямую без токенов как они прописаны в конфиге в output, 
  необходимо например для ретлянсляторов

Интеграция с ForkPlayer
access_referer - разрешить вход в плейлист с определенного адреса, указываем * если всем включая другие плеера кроме ForkPlayer 
  здесь http://forkplayer.tv/mylist/ создаем раздел, настраиваем разделу доступ по мак адресам или всем
  внутри добавляем ссылку на плейлист  http://server:port/playlist.m3u8 (весь плейлист)
  или http://server:port/playlist.m3u8?category=<Category Name> где <Category Name> указываем с settings-groups
  прописываем access_referer = {"http://mylist.obovse.ru/<Имя раздела>",}
limit_connections - количество одновременных потоков для одного токена, обычно достаточно 1-го
blocked_mac - закрыть доступ определенным мак адресам, empty - пустой мак адрес (может возникать если лист будут открывать напрямую или не в ForkPlayer)
  по умолчанию blocked_mac={"empty",}
