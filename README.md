# Site Bombear — guia rápido

Site institucional em HTML, CSS e JavaScript puro. Não tem build, framework nem instalação.

## Estrutura de pastas

```
bombear/  (raiz do repositório)
├── index.html            Página inicial (topo, categorias, quem somos, marcas, contato)
├── produtos.html         Tipos de produto por categoria (produtos.html#bombas, #piscina…)
├── quem-somos.html       Por trás da Bombear (história e pilares)
├── condominios.html      Página para síndicos e administradoras
├── README.md             Este guia
└── assets/
    ├── css/style.css     Layout e animações (não precisa mexer para trocar cor)
    ├── js/conteudo.js    ★ ÚNICO ARQUIVO PARA EDITAR: textos, cores, fontes, fotos, contatos
    ├── js/site.js        Monta as páginas a partir do conteudo.js
    └── img/              Logos da Bombear (e as fotos, quando houver)
```

## Trocar qualquer coisa: só `assets/js/conteudo.js`

| Quero mudar…                    | Onde, dentro de `conteudo.js`                     |
|---------------------------------|---------------------------------------------------|
| Cores                           | `tema.cores`                                       |
| Fontes                          | `tema.fontes` (nomes + link do Google Fonts)       |
| WhatsApp, telefone, endereço    | `contato`                                          |
| Horário e selo "Aberto agora"   | `contato.horarios` + `contato.horarioConfirmado`   |
| Palavras que giram no topo      | `hero.palavras`                                    |
| Categorias e abas               | `categorias`                                       |
| Marcas                          | `marcas.lista`                                     |
| Título e descrição do Google    | `seo`                                              |

**Fotos:** salve o arquivo em `assets/img/` (WebP, até ~300 KB) e troque
`{ src: null, alt: "…" }` por `{ src: "assets/img/fachada.webp", alt: "Fachada da loja" }`.
Enquanto o `src` for `null`, aparece um quadro "FOTO AQUI".

**Selo "Aberto agora":** só aparece quando `horarioConfirmado: true`. Preencha os
horários reais antes de ligar, senão o site diz "aberto" com a loja fechada.

## Pendências antes de publicar

Procure por `[` no `conteudo.js`. Cada `[COLCHETE]` é um dado que falta:
WhatsApp, telefone, CEP, e-mail, horário, Instagram, Facebook, domínio e imagem de compartilhamento.

## Fotos da loja (pendente até a loja ficar pronta)

Na página Quem Somos, a faixa com 4 fotos da loja está desligada. No lugar dela aparece o símbolo
da Bombear ao lado da nossa história. Quando a loja estiver montada:

1. Fotografe: fachada, showroom com bombas funcionando, equipe atendendo no balcão, prateleira de tubos e conexões.
2. Salve em `assets/img/` (WebP, até ~300 KB cada).
3. Em `conteudo.js` → `paginaQuemSomos.fotos`, preencha cada `src`.
4. Troque `paginaQuemSomos.mostrarFotos` para `true`.

## Testar no computador

```
cd bombear
python3 -m http.server 8000
```
Depois abra http://localhost:8000.

## Publicar

Funciona em qualquer hospedagem de site estático (GitHub Pages, Netlify, Hostinger).
Para o GitHub Pages: Settings → Pages → Branch `main`, pasta `/ (root)` → Save.

### Domínio próprio (bombear.org)

O arquivo `CNAME` na raiz diz ao GitHub Pages que o site responde em **bombear.org**.
No painel onde o domínio foi registrado, configure o DNS:

| Tipo  | Nome | Valor |
|-------|------|-------|
| A     | @    | 185.199.108.153 |
| A     | @    | 185.199.109.153 |
| A     | @    | 185.199.110.153 |
| A     | @    | 185.199.111.153 |
| CNAME | www  | businessdigitalmpe.github.io |

Atenção: se o e-mail @bombear.org já funciona, **não apague os registros MX** nem os TXT do e-mail.
Depois que o DNS propagar (de minutos a 24 h): Settings → Pages → marcar **Enforce HTTPS**.

## Limitação conhecida (SEO)

O conteúdo é montado por JavaScript para que tudo fique em um único arquivo. O Google
lê JavaScript, mas outros buscadores e as prévias de link no WhatsApp/Instagram leem
só o HTML: por isso título e descrição também estão escritos no `<head>` de cada página.
Se o tráfego orgânico virar prioridade, o próximo passo é gerar HTML estático a partir
do mesmo `conteudo.js`.
