# Como a gente trabalha nos repositórios da Adapt

## Branches

- A `main` é o que está no ar, ou pronto para ir.
- Ajuste pequeno pode ir direto na `main`. Mudança grande ganha uma branch (`ajuste/cardapio`, `bug/menu-iphone`) e um PR, para o checklist rodar antes de juntar.

## Commits

Em português, uma frase curta dizendo o que muda, sem ponto final. Se o commit mexe em mais de uma coisa, separe com ponto e vírgula.

```
Hero liso no iPhone; play some com o título
CI: Node 24 para casar com o lockfile do npm 11
```

## Antes de subir

```bash
npm test
npm run lint
npm run build
```

Se algum falhar, não sobe. O CI roda os mesmos passos em todo push e PR.

## Segredos

- Chave, token e senha nunca entram no código. Na máquina, ficam no `.env.local`, que o `.gitignore` já ignora.
- No CI, ficam em *Settings → Secrets and variables → Actions* do repositório.
- Se um segredo vazar num commit, troque o segredo primeiro e limpe o histórico depois.

## Cada projeto tem um CLAUDE.md

Na raiz de cada repositório, o `CLAUDE.md` diz o tipo do projeto, as decisões tomadas, as pendências com o cliente e o status. É a fonte da verdade do projeto: mudou alguma decisão, atualize ele no mesmo commit.

## Dado de negócio não se inventa

Preço, horário, endereço, telefone, nome de prato e depoimento só entram quando o cliente passa. Enquanto não chega, abra uma issue de **pendência do cliente** e deixe o lugar marcado no site.
