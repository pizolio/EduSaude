# 🍓 Edusaude

Bem-vindo ao **Edusaude**! Uma plataforma interativa e educativa focada em saúde, nutrição e bem-estar. Nosso objetivo é fornecer conhecimento de forma acessível e divertida através de aulas em vídeo, quizzes interativos e uma comunidade engajada.

## 📋 Sobre o Projeto

O Edusaude é uma aplicação web **Single Page Application (SPA)** simulada, construída com tecnologias web modernas. O design é inspirado em um piquenique, trazendo uma atmosfera leve e acolhedora para o aprendizado.

## 🚀 Funcionalidades

### 1. Autenticação e Perfis
- **Login e Cadastro:** Sistema seguro de autenticação utilizando **Supabase Auth**.
- **Metadados do Usuário:** Armazenamento do nome do usuário (`full_name`) para personalização da interface.
- **Proteção de Rotas:** Acesso restrito a funcionalidades como Fórum e Quiz apenas para usuários autenticados.

### 2. Dashboard Principal (`index.html`)
- **Vitrine de Temas:** Listagem dinâmica dos temas de estudo disponíveis.
- **Destaques:** Acesso rápido ao "Quiz em Destaque" e atalhos para a comunidade.
- **Design Responsivo:** Interface adaptável para dispositivos móveis e desktops.

### 3. Aulas Temáticas (`tema.html`)
- **Conteúdo em Vídeo:** Integração com vídeos do YouTube (embed) para aulas didáticas.
- **Navegação Intuitiva:** Cada tema possui sua página dedicada com lista de aulas e link direto para o quiz relacionado.

### 4. Quizzes Interativos (`quiz.html`)
- **Gamificação:** Teste seus conhecimentos com perguntas de múltipla escolha.
- **Feedback Imediato:** O sistema informa instantaneamente se a resposta está correta ou incorreta.
- **Pontuação:** Acompanhamento do placar em tempo real e tela de resultados ao final.

### 5. Fórum da Comunidade (`forum.html`)
- **Interação Social:** Espaço para os usuários tirarem dúvidas e compartilharem dicas.
- **Criação de Tópicos:** Formulário simples para iniciar novas discussões.
- **Sistema de Likes:** Funcionalidade de curtir tópicos, com contagem em tempo real e persistência no banco de dados.

## 🏗️ Arquitetura Técnica

O projeto segue uma arquitetura **Client-Side Rendering (CSR)**, onde o navegador é responsável por renderizar o conteúdo dinâmico obtido através da API do Supabase.

### Frontend
- **HTML5 & CSS3:** Estrutura semântica e estilização customizada.
- **TailwindCSS (via CDN):** Framework utilitário para estilização rápida, responsividade e consistência visual.
- **JavaScript (Vanilla ES6+):** Lógica da aplicação, manipulação do DOM e comunicação assíncrona com o backend.

### Backend & Infraestrutura
- **Supabase:** Plataforma Backend-as-a-Service (BaaS) que fornece:
    - **PostgreSQL:** Banco de dados relacional robusto.
    - **Authentication:** Gerenciamento de usuários e sessões (JWT).
    - **API Automática:** Interface RESTful/Realtime gerada automaticamente a partir do schema do banco.

## 💾 Banco de Dados (Schema)

O banco de dados PostgreSQL está estruturado com as seguintes tabelas principais:

### Conteúdo Educacional
- **`temas`**: Categorias de estudo.
    - `id` (UUID), `nome` (Text), `descricao` (Text)
- **`aulas`**: Vídeos educativos vinculados a um tema.
    - `id` (UUID), `tema_id` (FK), `titulo` (Text), `video_url` (Text)
- **`quizzes`**: Avaliações vinculadas a um tema.
    - `id` (UUID), `tema_id` (FK), `titulo` (Text)
- **`perguntas`**: Questões de um quiz.
    - `id` (UUID), `quiz_id` (FK), `texto_pergunta` (Text)
- **`respostas`**: Opções de resposta para uma pergunta.
    - `id` (UUID), `pergunta_id` (FK), `texto_resposta` (Text), `e_correta` (Boolean)

### Comunidade
- **`forum_posts`**: Tópicos de discussão criados pelos usuários.
    - `id` (UUID), `user_id` (UUID), `titulo` (Text), `conteudo` (Text), `author_name` (Text), `created_at` (Timestamp)
- **`post_likes`**: Registro de curtidas em tópicos (relação N:N entre usuários e posts).
    - `id` (UUID), `user_id` (UUID), `post_id` (FK)

## 🔌 API e Integração

A comunicação com o backend é feita através da biblioteca cliente oficial `@supabase/supabase-js`.

### Exemplo de Consumo (Listar Temas)
```javascript
const { data, error } = await supabaseClient
    .from('temas')
    .select('*');
```

### Exemplo de Autenticação (Login)
```javascript
const { data, error } = await supabaseClient.auth.signInWithPassword({
    email: 'usuario@exemplo.com',
    password: 'senha-secreta',
});
```

## 🏁 Como Executar

1. Clone este repositório ou baixe os arquivos.
2. Abra o arquivo `index.html` em seu navegador de preferência.
3. Crie uma conta ou faça login para acessar todas as funcionalidades.

---
&copy; 2025 Edusaude. Todos os direitos reservados.
