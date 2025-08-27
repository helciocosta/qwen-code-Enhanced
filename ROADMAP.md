# ROADMAP: Qwen-Code-Enhanced

Este documento descreve o plano de desenvolvimento para o fork **Qwen-Code-Enhanced**, uma versão aprimorada da ferramenta `qwen-code` com foco em autonomia (uso offline), personalização e eficiência para o desenvolvedor.

## Visão do Projeto

O objetivo é transformar o `qwen-code` em um assistente de codificação mais poderoso e flexível, que não dependa exclusivamente de uma conexão com a internet e que se adapte melhor aos fluxos de trabalho individuais do desenvolvedor.

---

## Fase 1: Fundação e Suporte Offline

O foco inicial é quebrar a dependência da nuvem e estabelecer as bases para futuras melhorias.

### 1.1. Criação do Fork e Limpeza Inicial
- [ ] **Criar o Fork:** Fazer o fork do repositório `QwenLM/qwen-code` no GitHub.
- [ ] **Clonar o Fork Localmente:** `git clone [URL-do-seu-fork]`
- [ ] **Renomear o Projeto:** Atualizar o `package.json` e outros locais relevantes para refletir o novo nome (ex: `qwen-code-enhanced`).
- [ ] **Revisar o Código:** Navegar pela estrutura do projeto para entender os principais componentes, especialmente os relacionados à autenticação e chamadas de API.

### 1.2. Implementar Suporte a Modelos Locais (Ollama/LM Studio)
Esta é a funcionalidade principal da Fase 1.

- [ ] **Modificar o Menu de Configuração:** Adicionar uma nova opção na interface de autenticação inicial: "3. Agente Local (Ollama/Outro)".
- [ ] **Criar Lógica de Configuração Local:**
    - Se a opção 3 for escolhida, solicitar ao usuário a URL base da API local (ex: `http://localhost:11434/v1` ).
    - Oferecer um valor padrão (`default`) para facilitar a configuração com o Ollama.
    - O nome do modelo a ser usado (ex: `codellama:7b`).
    - Salvar essas configurações no arquivo de configuração do projeto.
- [ ] **Adaptar o Cliente de API:** Modificar a função que faz as chamadas para a API para que ela use a URL base e o modelo configurados pelo usuário, em vez de se conectar à API da Qwen. A chave de API pode ser um valor fixo como "ollama", já que muitos servidores locais não a exigem.
- [ ] **Documentar o Uso Local:** Atualizar o `README.md` com instruções claras sobre como:
    - Instalar e executar o Ollama.
    - Baixar um modelo de codificação (`ollama pull codellama`).
    - Configurar a ferramenta para usar este modelo local.

---

## Fase 2: Melhorias de Usabilidade e Controle

Com o suporte local funcionando, o foco muda para dar mais controle e poder ao usuário.

### 2.1. Gerenciamento Explícito de Contexto
- [ ] **Implementar Comandos de Contexto:**
    - `/add <caminho_do_arquivo_ou_pasta>`: Adiciona o conteúdo de um ou mais arquivos ao contexto da conversa.
    - `/remove <caminho_do_arquivo>`: Remove um arquivo do contexto.
    - `/context`: Lista todos os arquivos atualmente no contexto.
    - `/clear`: Limpa todo o contexto da sessão atual.
- [ ] **Atualizar a Interface:** Exibir o número de arquivos e talvez o total de tokens do contexto atual no prompt da ferramenta.

### 2.2. Sistema de Personas (Prompts Customizáveis)
- [ ] **Criar Comandos de Persona:**
    - `/persona save <nome> "[PROMPT]"`: Salva um prompt de sistema customizado.
    - `/persona use <nome>`: Carrega o prompt para a sessão atual.
    - `/persona list`: Lista todas as personas salvas.
    - `/persona delete <nome>`: Apaga uma persona.
- [ ] **Armazenamento de Personas:** Salvar as personas em um arquivo de configuração global (ex: `~/.qwen-code-enhanced/personas.json`) para que estejam disponíveis em todos os projetos.

---

## Fase 3: Integração e Automação de Fluxos de Trabalho

O objetivo aqui é fazer com que a ferramenta realize tarefas complexas e se integre de forma mais inteligente com as ferramentas do desenvolvedor.

### 3.1. Integração Avançada com Git
- [ ] **Comando de Commit Inteligente:**
    - Criar o comando `qwen-enhanced commit`.
    - O comando deve executar `git diff --staged`, enviar o resultado para a IA e usar a resposta para gerar uma mensagem de commit seguindo as melhores práticas (Conventional Commits).
- [ ] **Comando de Revisão de Código:**
    - Criar o comando `qwen-enhanced review`.
    - O comando deve pegar as mudanças no branch atual (comparado ao `main` ou `develop`), enviá-las para a IA e pedir uma revisão de código, apontando possíveis bugs, melhorias de estilo ou vulnerabilidades.

### 3.2. Histórico de Conversas Persistente
- [ ] **Salvar Sessões:** Automaticamente salvar cada sessão de chat em um arquivo local (JSON ou SQLite).
- [ ] **Implementar Comandos de Histórico:**
    - `/history`: Lista as sessões anteriores com data e um resumo.
    - `/load <id_sessao>`: Carrega uma sessão anterior para continuar a conversa.
    - `/search <termo>`: Pesquisa em todo o histórico de conversas.

---

## Fase 4: Refinamento e Expansão (Ideias Futuras)

- [ ] **Suporte a Multimodalidade:** Se o modelo local suportar (ex: LLaVA), permitir que a ferramenta analise imagens.
- [ ] **Sistema de Plugins:** Arquitetar um sistema que permita que outros desenvolvedores criem e compartilhem plugins (novos comandos ou integrações).
- [ ] **Geração de Testes Automatizada:** Um comando como `/test <arquivo>` que lê um arquivo de código e gera automaticamente um arquivo de teste correspondente.
- [ ] **Interface Gráfica (GUI):** Considerar a criação de uma interface gráfica simples (usando Electron ou Tauri) como um companheiro para a CLI.


