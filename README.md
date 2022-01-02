    Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.
     >git log aefea
     aefead2207ef7e2aa5dc81a34aedf0cad4c32545    Update CHANGELOG.md  
    
    Какому тегу соответствует коммит 85024d3?
     >git log 85024d3 --oneline 
      (tag: v0.12.23)
    
    Сколько родителей у коммита b8d720? Напишите их хеши.
     >git log b8d720
      Merge: 56cd7859e 9ea88f22f
      
    Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.
     >git log v0.12.23..v0.12.24 --oneline
      33ff1c03b (tag: v0.12.24) v0.12.24
      b14b74c49 [Website] vmc provider links
      3f235065b Update CHANGELOG.md
      6ae64e247 registry: Fix panic when server is unreachable
      5c619ca1b website: Remove links to the getting started guide's old location
      06275647e Update CHANGELOG.md
      d5f9411f5 command: Fix bug when using terraform login on Windows
      4b6d06cc5 Update CHANGELOG.md
      dd01a3507 Update CHANGELOG.md
      225466bc3 Cleanup after v0.12.23 release
    
    Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).
     >git log -S "func providerSource("
      8c928e835
      
    Найдите все коммиты в которых была изменена функция globalPluginDirs.
     >git log --oneline -L :globalPluginDirs:plugins.go
      78b122055 Remove config.go and update things using its aliases
      52dbf9483 keep .terraform.d/plugins for discovery
      41ab0aef7 Add missing OS_ARCH dir to global plugin paths
      66ebff90c move some more plugin search path logic to command
      8364383c3 Push plugin discovery down into command package

      (END)
    
    Кто автор функции synchronizedWriters?
     >git log --reverse -S "synchronizedWriters"
      commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
      Author: Martin Atkins <mart@degeneration.co.uk>
