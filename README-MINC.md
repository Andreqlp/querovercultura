# Quero ver Cultura - Desktop

Visualizador para o canal da cultura utilizando [butter-desktop](https://github.com/butterproject/butter-desktop).


# Arquitetura


           ____
         |    |
         |____|-------------------------
    torrent tracker                    |
                 __                    |
       ___      |  |                  __
      |___|     |  |                 |  |
      |___|-----|__|                 |__|
    storage   bittorrent        provider http (vodo / json)
                               /      |
    ------------------------ / ------ | ---------
    client side            /          |
                       ___            |
                      |   |           _|
                      |___|          | |
                     /___/           |_|


# Partes:

1. Cliente - ex: butter-desktop
2. Servidor provider http (lista de filmes em json) -> http://querovercultura/
3. Servidor client torrent
4. Servidor tracker torrent 


# Cliente

## Configuração de ambiente

### Debian:

    $ sudo apt-get install npm nodejs-legacy
    $ sudo npm install -g bower grunt-cli grunt
    $ git clone https://github.com/culturagovbr/querovercultura.git
    $ git checkout minc/master
    $ cd querovercultura
    $ npm install
    $ bower install
    $ grunt build
    $ grunt start

# Provider http

O provedor é um arquivo no formato json com uma lista de itens com descritores dos arquivos de vídeo.

## Exemplo de arquivo json

```javascript
    {
	"downloads": [{
		"SizeByte": 1584818137,
		"Rating": 80,
		"Runtime": "70",
		"MovieUrl": "http://vodo.net/joshbernhard/lionshare/",
		"TorrentSeeds": "todo",
		"ImdbUrl": "http://www.imdb.com/title/tt1502421/",
		"CoverImage": "http://vodo.net/media/posters/poster_lionshare.jpg",
		"Popularity": 79,
		"TorrentUrl": "http://vodo.net/media/torrents/Lionshare.2009.Legacy.2008.720p.x264-VODO.torrent",
		"MovieRating": "6.2",
		"TorrentPeers": "todo",
		"Synopsis": "Finding love through filesharing! ",
		"Tagline": "Finding love through filesharing! ",
		"Genre": "indie,drama,filesharing",
		"Size": "768.0M",
		"Quality": "720p",
		"MovieTitleClean": "The Lionshare",
		"MovieYear": "2009",
		"ImdbCode": "tt1502421"
	},
        {}]
    }
```

Exemplo de provider http funcionando:

[](http://butter.vodo.net/popcorn)


# Cliente torrent

Esse é a máquina que armazena os arquivos e os seeda. Possui apenas um client torrent instalado e compartilha os arquivos do acervo.

    # apt-get install bittorrent
 
# Tracker torrent

Servidor que faz a função de tracker do torrent, isto é, auxiliar os nós de uma rede BitTorrent a encontrarem os arquivos.

[BitTorrent Tracker - wikipedia](https://en.wikipedia.org/wiki/BitTorrent_tracker)


# Dicas para desenvolvimento do cliente

## Para editar os templates

Crie um tema na pasta abaixo com o padrão [NOME_theme.styl]

    $ cd src/app/styl
    $ cp THEMENAME_theme.styl NOME_theme.styl


## Atualizando após alterações

Atualização completa:

    $ grunt build
    $ grunt start

Atualizando apenas templates:

    $ grunt shell:themes && grunt clean:css && grunt stylus:third_party

## Rodando sem grunt build

    $ ./cache/0.12.3/linux64/nw .

## Alterando o provider dos arquivos

    $ [editor] src/app/lib/providers/vodo.js
    
    var apiUrl = 'http://butter.vodo.net/popcorn',

# Referências

* [boilerplate](https://github.com/chentsulin/electron-react-boilerplate)
* [pĺayer](https://facebook.github.io/react/docs/jsx-in-depth.html)
* [desing](http://www.designideas.pics/popcorn-time-redesign-by-gabriel-mendes/)

