# Case Vitru · Protótipo da página de inscrição

Protótipo funcional da página de inscrição e da página de obrigado do lançamento da Pós-Graduação em Posicionamento Médico, feito para o case de Analista de Marketing Pleno (Web e Automações).

**Autor:** Josiel Silvério
**Página:** https://josielsn93.github.io/case-vitru-landing/

> Marca, pessoas e números são fictícios. Nenhum dado digitado sai do navegador: o envio ao n8n é simulado e aparece no painel técnico.

## Como avaliar em 2 minutos

1. Abra a página no celular.
2. Toque em **Painel técnico** e use **Simular visita: anúncio Instagram** para carregar a página com UTMs.
3. Preencha o formulário com dados errados (nome sem sobrenome, `ana@gmial.com`, telefone sem o 9) e veja as mensagens e sugestões.
4. Conclua as duas etapas e abra o painel de novo: ele mostra o `dataLayer`, o payload do webhook e a deduplicação Pixel × CAPI.
5. Abra `?view=obrigado` direto: a página aparece, mas nenhum lead é disparado.

## O que está implementado

| Item | Como funciona |
| --- | --- |
| Formulário em duas etapas | Etapa 1 cria o lead (nome, e-mail, WhatsApp, consentimento); etapa 2 qualifica (especialidade, situação do consultório) |
| Validação em tempo real | Valida ao sair do campo e revalida a cada tecla quando há erro; borda, ícone e mensagem, nunca só cor |
| WhatsApp | Máscara, DDD entre os 67 válidos, celular com 11 dígitos começando em 9, sugestão do nono dígito, recusa de fixo, saída em E.164 |
| E-mail | Formato e sugestão para erros comuns de domínio (gmial.com → gmail.com) |
| Especialidade | Combobox: 10 mais comuns ao tocar, filtro sem acento entre as 50 ao digitar, opção "Outra" |
| Consentimento LGPD | Checkbox desmarcado, obrigatório na etapa 1; payload leva versão do texto e data e hora |
| Cookies | Consent Mode v2 com tudo negado por padrão, atualizado pelo banner |
| UTMs | Primeiro toque em cookie (90 dias), último toque na sessão, campos ocultos no formulário |
| Eventos | `form_view`, `form_start`, `lead_submit` com `event_id` no sucesso do envio, `qualify_lead`, `thank_you_view` |
| Página de obrigado | Google Agenda, arquivo .ics com alerta 2 h antes, grupo de avisos, vídeo; pergunta a situação do consultório a quem pulou a etapa 2 |
| SEO | `noindex`, title, description, headings e dados estruturados Event, Course e FAQPage |
| UX celular | Uma coluna, fonte de 16 px nos campos, botão fixo que some perto do formulário e do rodapé |

## Diferença para produção

- A página seria montada em WordPress + Elementor Pro, com este HTML como referência ou num widget HTML.
- O envio iria para o webhook do n8n com token secreto no cabeçalho; o GTM real leria o `dataLayer`.
- A validação de telefone usaria a biblioteca libphonenumber-js, com as mesmas regras aplicadas aqui à mão.
- Política de privacidade, grupo de WhatsApp e vídeo são espaços reservados.

## Arquivos

- `index.html`: página única, sem dependências além da fonte do Google Fonts.
