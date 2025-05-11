# Catálogo de Produtos Android com Kotlin

## Descrição do Projeto

Este é um aplicativo Android nativo desenvolvido em Kotlin para gerenciar um catálogo de produtos. Ele permite aos usuários visualizar uma lista de produtos, ver detalhes de cada item, adicionar novos produtos (com a tentativa de anexar uma imagem), editar informações de produtos existentes e excluir produtos do catálogo.

O projeto demonstra o uso de tecnologias modernas do Android, como a arquitetura MVVM, Room para persistência de dados local, Navigation Component para navegação entre telas, Coroutines e StateFlow para programação assíncrona e reativa, RecyclerView para listas eficientes e Glide para carregamento de imagens.

## Autores

* Vitor Neres de Souza e Silva

## ✨ Funcionalidades Desenvolvidas

1.  **Listagem de Produtos:**
    * Exibe todos os produtos cadastrados no banco de dados local em uma lista rolável.
    * Cada item da lista tenta exibir a imagem do produto (se um URI de imagem foi salvo e ainda está acessível), nome e preço.
    * Utiliza `RecyclerView` para uma exibição otimizada e eficiente da lista.
    * Um Botão de Ação Flutuante (FAB) permite ao usuário navegar para a tela de adição de um novo produto.
    * Clicar em um item da lista leva o usuário para a tela de "Detalhes do Produto".

2.  **Detalhes do Produto:**
    * Apresenta informações completas sobre um produto selecionado: tenta exibir a imagem (se um URI de imagem foi salvo e ainda está acessível), nome, preço e descrição detalhada.
    * Oferece um botão "Editar Produto" que navega para a tela de edição, pré-carregando os dados do produto atual.
    * Inclui um botão "Excluir Produto" que permite remover o produto do catálogo.

3.  **Adicionar/Editar Produto:**
    * Um formulário permite ao usuário inserir ou modificar os detalhes de um produto, incluindo:
        * Nome do Produto (obrigatório)
        * Descrição do Produto (obrigatório)
        * Preço do Produto (obrigatório, formato numérico)
    * **Anexar Imagem (Funcionalidade Básica):**
        * Permite ao usuário selecionar uma imagem da galeria do dispositivo.
        * Exibe uma pré-visualização da imagem selecionada na tela de edição.
        * O URI (identificador da imagem) fornecido pelo sistema ao selecionar a imagem é salvo junto com os dados do produto. (Ver "Observações sobre a Funcionalidade de Imagem" abaixo para limitações).
    * Validação básica de entrada para campos obrigatórios e formato de preço.
    * Um botão "Salvar Produto" persiste as informações (seja um novo produto ou atualizações de um existente) no banco de dados local (Room).
    * Ao editar, o formulário é preenchido com os dados existentes do produto, incluindo a tentativa de carregar a imagem associada.
    * Após salvar com sucesso, o usuário é redirecionado para a tela de detalhes do produto (se estava editando) ou para a lista de produtos (se estava adicionando um novo produto a partir da tela de listagem).

4.  **Excluir Produto:**
    * A funcionalidade de exclusão é acessível a partir da tela de "Detalhes do Produto".
    * Um diálogo de confirmação é exibido para prevenir exclusões acidentais.
    * Após a confirmação do usuário, o produto é removido do banco de dados local (Room).
    * O usuário é redirecionado para a tela de listagem de produtos após a exclusão bem-sucedida.

5.  **Persistência de Dados:**
    * Todos os dados dos produtos, incluindo o URI da imagem selecionada (se houver), são salvos localmente usando a biblioteca Room Persistence (uma abstração sobre o SQLite).
    * Os dados permanecem disponíveis mesmo após o aplicativo ser fechado e reaberto, com ressalvas para a acessibilidade do URI da imagem (ver observações).

## 🛠️ Arquitetura e Tecnologias Utilizadas

* **Linguagem:** Kotlin
* **Arquitetura:** Model-View-ViewModel (MVVM) para uma clara separação de responsabilidades, facilitando a testabilidade e manutenção.
* **Interface do Usuário (UI):** Layouts XML do Android e Fragments.
* **Navegação:** Android Navigation Component para gerenciar o fluxo de navegação entre as diferentes telas (Fragments) de forma estruturada.
* **Operações Assíncronas:** Kotlin Coroutines para executar tarefas em segundo plano (como operações de banco de dados) sem bloquear a thread principal.
* **Gerenciamento de Estado Reativo:** `StateFlow` (principalmente) e `LiveData` (implicitamente através do `AndroidViewModel`) para permitir que a UI reaja automaticamente a mudanças nos dados.
* **Banco de Dados:** Room Persistence Library para um acesso robusto e eficiente ao banco de dados SQLite local.
* **Carregamento de Imagens:** Biblioteca Glide para tentar carregar, exibir e armazenar em cache imagens a partir dos URIs salvos.
* **View Binding:** Utilizado para acessar views nos layouts de forma segura quanto a nulos e tipos, reduzindo a necessidade de `findViewById`.
* **RecyclerView:** Para exibição eficiente de listas.

## 📝 Observações sobre a Funcionalidade de Imagem (Versão Atual)

* A funcionalidade de anexar imagem permite que o usuário selecione uma imagem da galeria e seu URI (identificador do arquivo no sistema) é salvo no banco de dados.
* A exibição da imagem nas telas de listagem e detalhes depende da validade e acessibilidade contínua desse URI pelo aplicativo.

## ⚙️ Instruções de Instalação e Execução

1.  **Pré-requisitos:**
    * Android Studio (versão estável mais recente recomendada, ex: Iguana, Jellyfish ou posterior).
    * JDK (Java Development Kit) 17 ou superior (geralmente vem embutido com o Android Studio).
    * Um Emulador Android configurado (API 36 ou superior) ou um Dispositivo Android físico (API 26 ou superior).


3.  **Abrir no Android Studio:**
    * Abra o Android Studio.
    * Selecione "Open" (ou "Open an Existing Project").
    * Navegue até a pasta raiz do projeto clonado/descompactado e selecione-a.

4.  **Sincronização do Gradle:**
    * O Android Studio irá detectar os arquivos Gradle e iniciar uma sincronização para baixar todas as dependências necessárias. Isso pode levar alguns minutos, dependendo da sua conexão com a internet.
    * Se a sincronização não iniciar automaticamente, você pode acioná-la clicando no ícone de elefante com uma seta para baixo na barra de ferramentas do Gradle, ou em "File" > "Sync Project with Gradle Files".

5.  **Compilar e Executar:**
    * Após a sincronização bem-sucedida, selecione a configuração de execução `app` no menu dropdown (geralmente já está selecionado).
    * Escolha um emulador ou dispositivo físico conectado como destino.
    * Clique no botão "Run 'app'" (o ícone de play verde ▶️) ou use o atalho `Shift + F10`.

6.  **Solução de Problemas Comuns:**
    * **Erro de SDK não encontrado:** Verifique se você tem o Android SDK especificado no `build.gradle (Module :app)` (campo `compileSdk`) instalado através do SDK Manager no Android Studio ("Tools" > "SDK Manager").
    * **Erro de `minSdk`:** O projeto está configurado para `minSdk = 34`. Certifique-se de que seu emulador/dispositivo atende a este requisito.

---
