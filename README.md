# Crypto Alert — testes E2E no Expo Web

Aplicativo React Native com Expo Router. A suíte em `.maestro/` cobre conversão de criptomoedas, criação e exclusão de alertas e validação do formulário de alerta.

## Preparação

É necessário Node.js, npm, Java 17 ou superior e a CLI do Maestro. No Windows, baixe o `maestro.zip` na [página de versões do Maestro](https://github.com/mobile-dev-inc/Maestro/releases), extraia para um diretório estável e adicione a pasta `maestro/bin` ao `PATH`. Confira a instalação:

```powershell
java -version
maestro --version
npm ci
```

## Executar o aplicativo e os testes

Em um terminal, na raiz do projeto:

```powershell
npx expo start --web --port 8081
```

Confirme que o Expo informa `http://localhost:8081` e que a página abre no navegador. Em outro terminal:

```powershell
maestro test .maestro/
```

Os quatro arquivos YAML usam `url: http://localhost:8081`. Caso o Expo escolha outra porta, atualize essa URL nos fluxos antes da execução. O Maestro Web abre sua própria instância de Chromium. As capturas produzidas pelos fluxos ficam no diretório de saída do Maestro.

Cada fluxo abre a aplicação e prepara suas próprias interações. O fluxo de exclusão cria seu alerta com preço gerado na própria execução e o remove pelo rótulo específico do botão. Como `clearState` não é oferecido pelo Maestro Web, a suíte não pressupõe uma lista de alertas vazia.

## Evidências

As capturas abaixo foram geradas por `takeScreenshot` durante a execução real no Chromium:

- [Conversão válida](evidencias/conversion-valid.png)
- [Alerta criado](evidencias/alert-created.png)

Validação em 04/11/2026: `maestro test .maestro/` concluiu com **4/4 fluxos aprovados** no Expo Web em `http://localhost:8081`. `npx tsc --noEmit` também concluiu sem erros.

## Escopo da validação

Esta suíte valida a versão **Expo Web no Chromium**. A execução Web não substitui a validação nativa que o enunciado acadêmico original solicita. Uma eventual validação em Android ou iOS deve ser registrada separadamente pelo estudante.

O planejamento assistido por IA está em [ia/planejamento.md](ia/planejamento.md). A reflexão acadêmica em `reflexao.md` é de responsabilidade exclusiva do estudante.
