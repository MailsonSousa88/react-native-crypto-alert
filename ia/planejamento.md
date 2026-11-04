# Planejamento de Testes E2E com IA Generativa

## 1. Objetivo

Utilizar a IA generativa como apoio para identificar e planejar cenários de testes end-to-end (E2E) para o aplicativo Crypto Alert, que serão implementados utilizando o Maestro.

A IA será utilizada para sugerir os cenários, mas a implementação e a validação dos testes serão realizadas com base no funcionamento real da aplicação.

## 2. Prompt utilizado

**Ferramenta:** ChatGPT (GPT-6)

**Prompt:**

> Analise o projeto React Native Crypto Alert:
>
> link do meu fork: https://github.com/MailsonSousa88/react-native-crypto-alert
>
> Com base nas funcionalidades existentes, proponha cenários de testes end-to-end (E2E) que possam ser automatizados utilizando o Maestro.
>
> Para cada cenário, apresente:
> - Nome do cenário;
> - Objetivo;
> - Etapas de execução;
> - Resultado esperado.
>
> Considere cenários positivos e negativos, priorizando as principais funcionalidades da aplicação. Não invente funcionalidades que não existam no projeto.

## 3. Resposta original da IA

A IA sugeriu os seguintes cenários de testes E2E:

### CT-01 — Listagem de criptomoedas

**Objetivo:** verificar se as criptomoedas são exibidas corretamente.

**Etapas:**
1. Abrir o aplicativo.
2. Acessar a aba `List`.
3. Aguardar o carregamento.
4. Verificar a exibição das criptomoedas.

**Resultado esperado:** a aplicação apresenta a listagem com nomes, símbolos e preços das criptomoedas.

### CT-02 — Conversão de criptomoedas

**Objetivo:** verificar se a conversão de valores funciona corretamente.

**Etapas:**
1. Acessar a aba `Convert`.
2. Informar `1` no campo `Amount`.
3. Selecionar `Bitcoin`.
4. Selecionar `USD`.
5. Verificar o resultado em `Converted Amount`.

**Resultado esperado:** a aplicação apresenta um valor convertido válido.

### CT-03 — Conversão com valor inválido

**Objetivo:** verificar o tratamento de valores inválidos na conversão.

**Etapas:**
1. Acessar `Convert`.
2. Informar `0` no campo `Amount`.
3. Verificar a mensagem apresentada.

**Resultado esperado:** a aplicação apresenta `Invalid amount`.

### CT-04 — Criação de alerta

**Objetivo:** verificar a criação de um alerta de preço.

**Etapas:**
1. Acessar `Alerts`.
2. Clicar em `New Alert` ou `Create Alert`.
3. Selecionar `Bitcoin`.
4. Informar `70000` no campo `Target Price (USD)`.
5. Selecionar `Above target price`.
6. Clicar em `Save Alert`.

**Resultado esperado:** o alerta é salvo e aparece na listagem.

### CT-05 — Exclusão de alerta

**Objetivo:** verificar a exclusão de um alerta existente.

**Etapas:**
1. Acessar `Alerts`.
2. Identificar um alerta.
3. Clicar no botão de exclusão.
4. Verificar a listagem.

**Resultado esperado:** o alerta selecionado é removido da aplicação.

### CT-06 — Persistência dos alertas

**Objetivo:** verificar se os alertas continuam salvos após reiniciar a aplicação.

**Etapas:**
1. Criar um alerta.
2. Confirmar sua presença na listagem.
3. Fechar e abrir novamente a aplicação.
4. Acessar `Alerts`.

**Resultado esperado:** o alerta permanece disponível.

### CT-07 — Formulário de alerta inválido

**Objetivo:** verificar se o aplicativo impede a criação de alertas com dados inválidos.

**Etapas:**
1. Acessar `Create Alert`.
2. Manter o formulário vazio.
3. Verificar o botão `Save Alert`.
4. Informar `0` no campo de preço.
5. Verificar novamente o botão.

**Resultado esperado:** o botão permanece desabilitado e nenhum alerta inválido é criado.

### CT-08 — Navegação entre telas

**Objetivo:** verificar a navegação entre as funcionalidades principais.

**Etapas:**
1. Acessar `List`.
2. Navegar até `Convert`.
3. Navegar até `Alerts`.
4. Retornar à tela `List`.

**Resultado esperado:** todas as telas são acessadas corretamente.

## 4. Cenários selecionados

Foram selecionados quatro cenários para implementação com o Maestro.

| ID | Cenário | Arquivo |
|---|---|---|
| CT-02 | Conversão de criptomoedas | `01-conversion.yaml` |
| CT-04 | Criação de alerta | `02-create-alert.yaml` |
| CT-05 | Exclusão de alerta | `03-delete-alert.yaml` |
| CT-07 | Formulário inválido | `04-invalid-alert.yaml` |

Os cenários foram escolhidos por envolverem funcionalidades importantes da aplicação, incluindo preenchimento de campos, interação com botões, navegação e validação de resultados.

Os testes serão armazenados na pasta `.maestro/`.

## 5. Análise crítica

### O que foi aproveitado?

Foram aproveitados os cenários que representam funcionalidades reais do Crypto Alert e que permitem verificar o comportamento da aplicação através da interface.

Os testes de conversão, criação e exclusão de alertas e validação de formulário foram selecionados por cobrirem diferentes tipos de interação.

### O que foi corrigido?

No cenário de conversão, não será utilizado um valor fixo como resultado esperado, pois os preços das criptomoedas podem variar.

No cenário de exclusão, o teste deverá criar seu próprio alerta antes de excluí-lo, evitando depender de dados existentes ou de outros testes.

No formulário inválido, a verificação deve considerar que o botão `Save Alert` permanece desabilitado quando os dados não são válidos.

### O que foi descartado?

O cenário de listagem não foi priorizado porque depende da API externa CoinGecko, que pode apresentar falhas ou indisponibilidade.

O teste de persistência não foi selecionado inicialmente por exigir um controle maior sobre o armazenamento local.

O teste de navegação também não foi selecionado porque os demais cenários já envolvem a navegação entre telas.

O cenário de conversão inválida foi mantido como possibilidade de teste adicional, já que o formulário de alerta inválido permite verificar um comportamento semelhante de validação.

### Limitações da IA

A IA conseguiu propor cenários com base nas funcionalidades identificadas no código, mas isso não garante que os testes funcionem corretamente.

Os seletores, as ações e os resultados esperados precisam ser verificados durante a execução real.

Por isso, os cenários gerados serão utilizados como base para a implementação com Maestro, passando por revisão e ajustes quando necessário.

## 6. Validação dos cenários

Os testes serão implementados utilizando **Maestro Web**, com o Crypto Alert executado através do Expo Web no navegador Chromium.

A validação será realizada por meio da execução dos arquivos YAML, verificando se as ações e os resultados correspondem ao comportamento esperado.

- [ ] Implementar os quatro fluxos.
- [ ] Verificar os seletores na interface real.
- [ ] Executar os testes com Maestro.
- [ ] Corrigir possíveis problemas.
- [ ] Registrar evidências de pelo menos dois fluxos.

**Observação:** a execução Web será documentada separadamente, pois o enunciado original também exige validação em ambiente nativo.

## 7. Revisão durante a implementação

- O arquivo de planejamento foi colocado em `ia/planejamento.md`, preservando integralmente o prompt, a resposta original e os cenários selecionados acima.
- A execução foi configurada para a URL real informada pelo Expo Web neste ambiente: `http://localhost:8081`.
- No modal de seleção de criptomoeda da versão Web, o Maestro identificou a opção na árvore acessível, mas calculou a área de toque deslocada. Os fluxos de alerta usam um ponto relativo à tela para selecionar a primeira opção, Bitcoin, e verificam em seguida que `Bitcoin (BTC)` aparece no campo. Essa é uma exceção localizada à preferência por seletores textuais.
- A árvore acessível do Maestro Web não expôs o estado `enabled` do `Save Alert` no React Native Web. Os fluxos verificam o resultado observável: o formulário válido salva e aparece na lista; os formulários inválidos permanecem em `Create Alert` após o toque no botão e não geram alerta de preço zero.
- Na exclusão, o botão expôs seu `accessibilityLabel` em vez de `testID`. O rótulo foi tornado específico para criptomoeda e preço, e o fluxo gera um preço próprio para identificar o alerta criado mesmo com dados persistidos de execuções anteriores.
- Em 04/11/2026, a execução final de `maestro test .maestro/` no Chromium concluiu com **4/4 fluxos aprovados em 2 min 39 s**. As capturas reais de conversão e criação de alerta foram salvas em `evidencias/`.
