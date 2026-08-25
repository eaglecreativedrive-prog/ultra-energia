# LP Ultra Energia — captação de leads

Página única, estática, para rodar com tráfego pago (Meta e Google).

## Estrutura

```
lp-ultra-energia/
  index.html      página inteira (HTML + CSS + JS num arquivo só)
  assets/         logos e fotos de obra reais
```

## Como publicar

Sobe a pasta inteira em qualquer hospedagem estática (Vercel, Netlify, Hostinger, um
subdomínio tipo `solar.ultraenergia.com.br`). Não precisa de servidor nem banco.

Para testar local:

```
python3 -m http.server 8931 --directory lp-ultra-energia
```

## Para onde vão os leads

Tudo vai para o WhatsApp **(48) 99219-7177**, na constante `WHATSAPP` do `<script>` final.

- **Formulário:** valida os campos e monta a mensagem com nome, telefone, cidade, tipo
  de imóvel e faixa da conta de luz.
- **Botões de CTA:** vão direto para o WhatsApp com uma mensagem curta já escrita,
  para quem não quer preencher nada. A mensagem fica no atributo `data-wa` de cada
  botão e o ponto da página no `data-origem`.

Toda mensagem leva junto a linha `Origem:`, com o ponto de clique e a campanha (UTM) —
é assim que se descobre qual botão e qual anúncio trouxeram o cliente.

Limitação conhecida: o lead só chega se a pessoa apertar enviar no WhatsApp. Se quiser
capturar todo mundo que preencheu, dá para acoplar um endpoint (Formspree, Google Sheets
ou uma rota no portal-eagle) antes do `window.open` — o payload já está montado no array `l`.

## Antes de subir a campanha

1. **Pixels.** Colar o Meta Pixel e a tag do Google Ads no bloco marcado no `<head>`.
2. **Evento de conversão.** Descomentar as duas linhas `fbq('track','Lead')` e
   `gtag('event','generate_lead')` no `<script>` — sem isso o Meta não otimiza por lead.
3. **UTM nos anúncios.** A página já lê `utm_source`, `utm_medium`, `utm_campaign`,
   `utm_content` e `utm_term` e manda junto na mensagem. É assim que se descobre qual
   criativo trouxe o cliente.
4. **Trocar as fotos** quando houver obra nova (`assets/obra-01..06.jpg`, 4:3).

## Regras de marca aplicadas

- Paleta do briefing: índigo `#241E63` / `#1A1547`, off-white `#F2F3F7`, verde-limão
  `#8CC63F`, verde escuro `#5F9420` sobre fundo claro.
- Anton em caixa alta nos títulos, Inter no texto; ênfase só por cor, nunca itálico.
- Cards arredondados flutuando sobre fundo colorido — nada de texto em fundo chapado.
- Fotos reais de obra da equipe, sem banco de imagem e sem clichê de pôr do sol.
- **Sem promessa de percentual de economia** em nenhum ponto da página.
- Atendimento declarado **somente Santa Catarina**.
- CTA fixo "Fale com nosso time comercial".
- Privacidade: nenhuma foto ou legenda traz nome, rua ou bairro de cliente.

O FAQ responde às objeções técnicas com a versão correta do representante comercial:
telhado norte primeiro e leste/oeste como melhor saída; string em 9 de cada 10 casos;
e a sombra afetando só a sub-string por causa dos diodos de bypass.

## Prévia de investimento

A seção de preços replica o criativo do anúncio: três faixas de conta de luz (R$ 500,
R$ 800 e R$ 1.000), o número de painéis e a parcela inicial de cada uma, mais os 90 dias
de carência. Os valores estão escritos direto no HTML, na seção `INVESTIMENTO`.

**Sempre que a tabela do financiamento mudar, esses números precisam ser atualizados
aqui e no criativo ao mesmo tempo.** A ressalva "valores sujeitos a análise de crédito"
e a frase sobre o dimensionamento real não podem sair — são o que separa a prévia de
uma promessa de preço.

## Onde ficam os pontos de clique

São 15 destinos, todos no mesmo número, cada um com mensagem e `data-origem`
próprios. A linha `Origem:` que chega no WhatsApp diz de qual deles a pessoa veio —
use isso depois de duas semanas de campanha para cortar os que não convertem.

- topo, barra fixa do celular e ícone ao lado dela
- uma por faixa de preço (R$ 500, R$ 800 e R$ 1.000)
- uma ao fim de cada seção: diferenciais, problemas, processo, frentes, obras e FAQ
- rodapé, contato do rodapé e o botão flutuante de WhatsApp

O botão flutuante só aparece no desktop, depois que o hero sai da tela. No celular ele
sairia por cima da barra fixa, então lá o ícone fica dentro da própria barra.
