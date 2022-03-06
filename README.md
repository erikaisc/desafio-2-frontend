![](https://i.imgur.com/xG74tOh.png)

# Desafio | Front-end - Módulo 2

Você acabou de ser contratado pela melhor empresa de tecnologia do mundo: a **CUBOS**.
Sua primeira tarefa como desenvolvedor é criar uma aplicação para um serviço de streaming (pense num Netflix).

Seu papel é construir um website com [o seguinte design](https://www.figma.com/file/AL6hZ3Lq16Uj8mw1o4BzAK/Desafio-front-academy-2?node-id=0%3A1) que permita: (funcionalidades com * ao lado são obrigatórias)

- Visualização de filmes (*)
- Paginação de filmes (*)
- Busca de filmes (*)
- "Filme do dia" (*)
- Modal de filme (*)
- Mudança de tema

Os dados do website serão requisitados da [seguinte API](https://tmdb-proxy.cubos-academy.workers.dev/3/)

## Detalhamentos de Requisitos

### Visualização de filmes

Assim que o website for aberto, a listagem de filmes deverá ser preenchida com as informações do [seguinte endpoint](https://tmdb-proxy.cubos-academy.workers.dev/3/discover/movie?language=pt-BR&include_adult=false)

Exemplo de retorno:

```json
{
  "results": [
    {
      "adult": false,
      "backdrop_path": "https://image.tmdb.org/t/p/original/jlGmlFOcfo8n5tURmhC7YVd4Iyy.jpg",
      "genre_ids": [
        28,
        12,
        14
      ],
      "id": 436969,
      "original_language": "en",
      "original_title": "The Suicide Squad",
      "overview": "Os supervilões Harley Quinn (Margot Robbie), Bloodsport (Idris Elba), Peacemaker (John Cena) e uma coleção de malucos condenados da prisão de Belle Reve juntam-se à super-secreta e super-obscura Força Tarefa X, enquanto são deixados na remota ilha de Corto Maltese para combater o inimigo.",
      "popularity": 6294.822,
      "poster_path": "https://image.tmdb.org/t/p/original/wTS3dS2DJiMFFgqKDz5fxMTri.jpg",
      "release_date": "2021-07-28",
      "title": "O Esquadrão Suicida",
      "video": false,
      "vote_average": 8.1,
      "vote_count": 2435,
      "price": 10
    },
    {
      "adult": false,
      "backdrop_path": "https://image.tmdb.org/t/p/original/7WJjFviFBffEJvkAms4uWwbcVUk.jpg",
      "genre_ids": [
        12,
        14,
        35,
        28
      ],
      "id": 451048,
      "original_language": "en",
      "original_title": "Jungle Cruise",
      "overview": "O destemido capitão Frank Wolff e a intrépida pesquisadora Lily Houghton se aventuram pela Amazônia a bordo da peculiar embarcação La Quila. Determinados a encontrar uma árvore cujos poderes de cura podem mudar o futuro da medicina, nem mesmo as águas perigosas e as forças sobrenaturais que enfrentam pelo caminho poderão detê-los. Mas os riscos aumentam ainda mais conforme os segredos da árvore se revelam, o destino de Lily e Frank e também de toda a humanidade está em jogo.",
      "popularity": 5788.065,
      "poster_path": "https://image.tmdb.org/t/p/original/9E76j2DcQv8LdbX1Wa9jpbDBfw1.jpg",
      "release_date": "2021-07-28",
      "title": "Jungle Cruise",
      "video": false,
      "vote_average": 7.9,
      "vote_count": 1801,
      "price": 3.5
    }
  ]
}
```

A estrutura HTML deverá ser a seguinte:
![](https://i.imgur.com/s8j6m3E.png)

Informações do retorno da API necessárias para o preenchimento:
- background-image da `<div class="movie">` === poster_path
- texto do `<span class="movie__title">` === title
- texto do `<span class="movie__rating">` === vote_average

Essa estrutura terá que ser criada para **cada filme** poderá ser construida dinamicamente pela DOM, porém, isso **não é obrigatório**.

Cada filme deverá ser colocado dentro da `<div class="movies">`

### Paginação de filmes

Você poderá assumir que sempre existirão 4 páginas (0, 1, 2, 3) por conta do número de filmes em média ser 20 e, seu website sempre irá mostrar no máximo 5 por vez.

O `<button class="btn-prev">`, quando clicado, se não estiver na página 0, terá que voltar 1 página, se não, levará o usuário para a página 3
O `<button class="btn-next">`, quando clicado, se não estiver na página 3, terá que avançar 1 página, se não, levará o usuário para a página 0

Ao voltar ou avançar uma página, os filmes em tela serão atualizados corretamente.

### Busca de filmes

O usuário poderá buscar um filme por meio do `<input class="input">`

Quando o usuário pressionar a tecla "Enter" enquanto estiver com foco no inputm, algumas coisas teram que acontecer:
- O usuário terá que ser levado para a página 0
- Se o input possuir algum valor, você deverá realizar uma busca [no endpoint](https://tmdb-proxy.cubos-academy.workers.dev/3/search/movie?language=pt-BR&include_adult=false) passando um parametro de query "query" com o valor do input. Ex: Buscando por Matrix https://tmdb-proxy.cubos-academy.workers.dev/3/search/movie?language=pt-BR&include_adult=false&**query=Matrix**
- Se o input não possuir valor nenhum, você deverá realizar a mesma busca que é feita para preencher os filmes iniciais (Visualização de filmes)
- O valor do input terá que ser limpo

### "Filme do dia"

Assim que o website for aberto, o filme do dia deverá ser preenchido com as informações do [endpoint geral](https://tmdb-proxy.cubos-academy.workers.dev/3/movie/436969?language=pt-BR) e do [endpoint de videos](https://tmdb-proxy.cubos-academy.workers.dev/3/movie/436969/videos?language=pt-BR);

Exemplo de retorno:

**Endpoint Geral**
```json
{
  "adult": false,
  "backdrop_path": "https://image.tmdb.org/t/p/original/jlGmlFOcfo8n5tURmhC7YVd4Iyy.jpg",
  "belongs_to_collection": {
    "id": 531242,
    "name": "Suicide Squad Collection",
    "poster_path": "https://image.tmdb.org/t/p/original/bdgaCpdDh0J0H7ZRpDP2NJ8zxJE.jpg",
    "backdrop_path": "https://image.tmdb.org/t/p/original/e0uUxFdhdGLcvy9eC7WlO2eLusr.jpg"
  },
  "budget": 180000000,
  "genres": [
    {
      "id": 28,
      "name": "Ação"
    },
    {
      "id": 12,
      "name": "Aventura"
    },
    {
      "id": 14,
      "name": "Fantasia"
    }
  ],
  "homepage": "https://www.thesuicidesquad.net",
  "id": 436969,
  "imdb_id": "tt6334354",
  "original_language": "en",
  "original_title": "The Suicide Squad",
  "overview": "Os supervilões Harley Quinn (Margot Robbie), Bloodsport (Idris Elba), Peacemaker (John Cena) e uma coleção de malucos condenados da prisão de Belle Reve juntam-se à super-secreta e super-obscura Força Tarefa X, enquanto são deixados na remota ilha de Corto Maltese para combater o inimigo.",
  "popularity": 6294.822,
  "poster_path": "https://image.tmdb.org/t/p/original/wTS3dS2DJiMFFgqKDz5fxMTri.jpg",
  "production_companies": [
    {
      "id": 9993,
      "logo_path": "https://image.tmdb.org/t/p/original/2Tc1P3Ac8M479naPp1kYT3izLS5.png",
      "name": "DC Entertainment",
      "origin_country": "US"
    },
    {
      "id": 128064,
      "logo_path": "https://image.tmdb.org/t/p/original/13F3Jf7EFAcREU0xzZqJnVnyGXu.png",
      "name": "DC Films",
      "origin_country": "US"
    },
    {
      "id": 507,
      "logo_path": "https://image.tmdb.org/t/p/original/z7H707qUWigbjHnJDMfj6QITEpb.png",
      "name": "Atlas Entertainment",
      "origin_country": "US"
    },
    {
      "id": 429,
      "logo_path": "https://image.tmdb.org/t/p/original/2Tc1P3Ac8M479naPp1kYT3izLS5.png",
      "name": "DC Comics",
      "origin_country": "US"
    },
    {
      "id": 11565,
      "logo_path": null,
      "name": "The Safran Company",
      "origin_country": "US"
    },
    {
      "id": 174,
      "logo_path": "https://image.tmdb.org/t/p/original/IuAlhI9eVC9Z8UQWOIDdWRKSEJ.png",
      "name": "Warner Bros. Pictures",
      "origin_country": "US"
    }
  ],
  "production_countries": [
    {
      "iso_3166_1": "US",
      "name": "United States of America"
    }
  ],
  "release_date": "2021-07-28",
  "revenue": 118084747,
  "runtime": 132,
  "spoken_languages": [
    {
      "english_name": "English",
      "iso_639_1": "en",
      "name": "English"
    },
    { 
      "english_name": "Spanish",
      "iso_639_1": "es",
      "name": "Español"
    }
  ],
  "status": "Released",
  "tagline": "Eles estão loucos... para salvar o mundo.",
  "title": "O Esquadrão Suicida",
  "video": false,
  "vote_average": 8.1,
  "vote_count": 2469
}
```

**Endpoint de videos**
```json
{
  "id": 436969,
  "results": [
    {
      "iso_639_1": "pt",
      "iso_3166_1": "BR",
      "name": "O Esquadrão Suicida | Trailer Oficial | Legendado",
      "key": "VO_oW4GDy7o",
      "site": "YouTube",
      "size": 1080,
      "type": "Trailer",
      "official": false,
      "published_at": "2021-03-26T17:12:53.000Z",
      "id": "605e1ae71065d3003d9a23f7"
    },
    {
      "iso_639_1": "pt",
      "iso_3166_1": "BR",
      "name": "O Esquadrão Suicida - Trailer Restrito Oficial",
      "key": "Ch6DQDFbovI",
      "site": "YouTube",
      "size": 1080,
      "type": "Trailer",
      "official": true,
      "published_at": "2021-03-26T16:00:03.000Z",
      "id": "605e0aea8c31590029451a47"
    }
  ]
}
```

A estrutura HTML deverá ser a seguinte:
![](https://i.imgur.com/72ixMvR.png)

Informações do retorno do **Endpoint Geral** necessárias para o preenchimento:
- background-image da `<div class="highlight__video">` === backdrop_path
- texto do `<h3 class="highlight__title">` === title
- texto do `<span class="highlight__rating">` === vote_average
- texto do `<span class="highlight__genres">` === genres (como genres é um array de objetos, você deverá criar uma string concatenando todos os valores de genre.name e separando-os por vírgula)
- texto do `<span class="highlight__launch">` === release_date (como release_date é uma data, você **poderá** transforma-lá em outro formato)
- texto do `<p class="highlight__description">` === overview

Informações do retorno do **Endpoint de vídeos** necessárias para o preenchimento:
- href do `<a class="highlight__video-link">` === concatene a string "https://www.youtube.com/watch?v=" com o valor de **key** (como o Endpoint de vídeos retorna um array, você deverá pegar o valor de **key** do primeiro item)

### Modal de filme

Ao clicar na `<div class="movie">` a `<div class="modal hidden">` deverá perder a classe "hidden" (isso irá **abrir** o modal)

Assim que o modal for **aberto**, ele deverá ser preenchido com as informações do [seguinte endpoint](https://tmdb-proxy.cubos-academy.workers.dev/3/movie/?language=pt-BR) passando um parametro de rota com o valor do **id** do filme. Ex: Buscando pelo filme com id 436969 https://tmdb-proxy.cubos-academy.workers.dev/3/movie/**436969**?language=pt-BR

Exemplo de retorno:

```json
{
  "adult": false,
  "backdrop_path": "https://image.tmdb.org/t/p/original/jlGmlFOcfo8n5tURmhC7YVd4Iyy.jpg",
  "belongs_to_collection": {
    "id": 531242,
    "name": "Suicide Squad Collection",
    "poster_path": "https://image.tmdb.org/t/p/original/bdgaCpdDh0J0H7ZRpDP2NJ8zxJE.jpg",
    "backdrop_path": "https://image.tmdb.org/t/p/original/e0uUxFdhdGLcvy9eC7WlO2eLusr.jpg"
  },
  "budget": 180000000,
  "genres": [
    {
      "id": 28,
      "name": "Ação"
    },
    {
      "id": 12,
      "name": "Aventura"
    },
    {
      "id": 14,
      "name": "Fantasia"
    }
  ],
  "homepage": "https://www.thesuicidesquad.net",
  "id": 436969,
  "imdb_id": "tt6334354",
  "original_language": "en",
  "original_title": "The Suicide Squad",
  "overview": "Os supervilões Harley Quinn (Margot Robbie), Bloodsport (Idris Elba), Peacemaker (John Cena) e uma coleção de malucos condenados da prisão de Belle Reve juntam-se à super-secreta e super-obscura Força Tarefa X, enquanto são deixados na remota ilha de Corto Maltese para combater o inimigo.",
  "popularity": 6294.822,
  "poster_path": "https://image.tmdb.org/t/p/original/wTS3dS2DJiMFFgqKDz5fxMTri.jpg",
  "production_companies": [
    {
      "id": 9993,
      "logo_path": "https://image.tmdb.org/t/p/original/2Tc1P3Ac8M479naPp1kYT3izLS5.png",
      "name": "DC Entertainment",
      "origin_country": "US"
    },
    {
      "id": 128064,
      "logo_path": "https://image.tmdb.org/t/p/original/13F3Jf7EFAcREU0xzZqJnVnyGXu.png",
      "name": "DC Films",
      "origin_country": "US"
    },
    {
      "id": 507,
      "logo_path": "https://image.tmdb.org/t/p/original/z7H707qUWigbjHnJDMfj6QITEpb.png",
      "name": "Atlas Entertainment",
      "origin_country": "US"
    },
    {
      "id": 429,
      "logo_path": "https://image.tmdb.org/t/p/original/2Tc1P3Ac8M479naPp1kYT3izLS5.png",
      "name": "DC Comics",
      "origin_country": "US"
    },
    {
      "id": 11565,
      "logo_path": null,
      "name": "The Safran Company",
      "origin_country": "US"
    },
    {
      "id": 174,
      "logo_path": "https://image.tmdb.org/t/p/original/IuAlhI9eVC9Z8UQWOIDdWRKSEJ.png",
      "name": "Warner Bros. Pictures",
      "origin_country": "US"
    }
  ],
  "production_countries": [
    {
      "iso_3166_1": "US",
      "name": "United States of America"
    }
  ],
  "release_date": "2021-07-28",
  "revenue": 118084747,
  "runtime": 132,
  "spoken_languages": [
    {
      "english_name": "English",
      "iso_639_1": "en",
      "name": "English"
    },
    {
      "english_name": "Spanish",
      "iso_639_1": "es",
      "name": "Español"
    }
  ],
  "status": "Released",
  "tagline": "Eles estão loucos... para salvar o mundo.",
  "title": "O Esquadrão Suicida",
  "video": false,
  "vote_average": 8.1,
  "vote_count": 2469
}
```

A estrutura HTML deverá ser a seguinte:
![](https://i.imgur.com/quJYytr.png)

Informações do retorno da API necessárias para o preenchimento:
- texto do `<h3 class="modal__title">` === title
- src da `<img class="modal__img">` === backdrop_path
- texto do `<p class="modal__description">` === overview
- texto da `<div class="modal__average">` === vote_average
- **ISSO NÃO É OBRIGATÓRIO**
  - para cada genre, você deverá criar um `<span class="modal__genre">`, colocar como texto o valor de genre.name e adicioná-lo na `<div class="modal__genres">`

O modal poderá ser "fechado" por meio de um clique nele próprio ou na `<img class="modal__close">`, ao clicar em qualquer um dos dois, a classe "hidden" deverá ser adicionada a `<div class="modal">`

### Mudança de tema **NÃO OBRIGATÓRIO**

Ao clicar na `<img class="btn-theme">`, caso o **tema atual** seja "light" ou "claro", o mesmo deverá ser trocado para o tema "dark" ou "escuro", após isso, você deverá modificar o tema (imagens e cores) do seu website de acordo com o Figma. Essa troca de tema, poderá ser facilitada caso seja feita por meio da troca de variáveis CSS.

## Aulas úteis:

-   [Selecionando elementos mais facilmente](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/06/01/2022/aula/dcf79bd9-3872-43ed-b4e9-8488cbb9b4ae/1427ba35-c47d-4292-965e-62424ea1ec60)
-   [Modificando as propriedades dos elementos](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/06/01/2022/aula/dcf79bd9-3872-43ed-b4e9-8488cbb9b4ae/61861a59-a16a-4099-ba2d-eb1559032382)
-   [Manipulando classes com a DOM](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/06/01/2022/aula/dcf79bd9-3872-43ed-b4e9-8488cbb9b4ae/7cf34531-5a18-4e1d-8105-13ea74c28e1e)
-   [Evento de clique](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/06/01/2022/aula/dcf79bd9-3872-43ed-b4e9-8488cbb9b4ae/07fed18a-2068-468a-83fe-9bf84673dbf5)
-   [Evento de Tecla e objeto de eventos](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/11/01/2022/aula/62543c16-2009-48b8-afbf-177816a3983d/850f8dc8-c3c7-4ab9-8785-254e7f0ea038)
-   [Target e multiplos eventos](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/11/01/2022/aula/62543c16-2009-48b8-afbf-177816a3983d/5cb2d4cd-3818-46a3-90ac-02e82a4e4e85)
-   [Resumo position fixed](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/13/01/2022/aula/7728a384-e8de-47d1-bb36-17b649929e45/c9c5539f-7d5a-471f-8da6-156dfbe40ea5)
-   [Criando um modal](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/13/01/2022/aula/7728a384-e8de-47d1-bb36-17b649929e45/82ecad86-e014-467f-a855-16567607dbf4)
-   [Fetch e assincronismo](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/25/01/2022/aula/590ceddc-0cfa-4d67-9435-b6d724080c86/5c1e8d1b-e6bd-4d43-849e-11b47c1ddc88)
-   [Populando a página com informações externas](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/27/01/2022/aula/bd37b412-5904-4a95-8e73-29da894e09da/da42bf0d-bc6d-4159-b880-902e430faa5e)
-   [Criando e adicionando elementos](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/27/01/2022/aula/bd37b412-5904-4a95-8e73-29da894e09da/098d8118-35e0-43b0-9bb3-fc0a6b376e1b)
-   [Variaveis CSS](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/01/02/2022/aula/86d6b72e-9846-405b-9d1a-9ba61be33e3e/6267a54e-5410-410a-80aa-1d65b01484e0)
-   [Modificando as variaveis CSS pelo DOM](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/01/02/2022/aula/86d6b72e-9846-405b-9d1a-9ba61be33e3e/c84dbae3-f2fd-428d-bc05-da55a8edad05)
-   [LocalStorage](https://plataforma.cubos.academy/curso/6e938100-e6dd-4b5d-a018-61a62ba2429b/data/01/02/2022/aula/86d6b72e-9846-405b-9d1a-9ba61be33e3e/fc81a87c-65d7-4e17-8b28-d0a67139cd90)

**LEMBRE-SE**: é melhor feito do que perfeito!!!

###### tags: `front-end` `módulo 2` `HTML` `DOM` `CSS` `desafio`
