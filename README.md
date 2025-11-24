# landpage

🚀 PROSOLUTIONS: Landing Page de Alta Conversão

Esta é uma Landing Page profissional de alto impacto, projetada para capturar leads (contactos) e apresentar uma proposta de valor clara para serviços de desenvolvimento web. O foco principal é na velocidade, escalabilidade e prova social, com um sistema de chat em tempo real integrado.

Funcionalidades Principais

Design Responsivo e Moderno: Construído com Tailwind CSS e a fonte Inter, garantindo uma experiência de utilizador fluida em qualquer dispositivo.

Proposta de Valor Clara (Hero): Título focado no resultado do cliente ("Lance o Seu Produto Digital em 4 Semanas").

Chamada à Ação (CTA) em Destaque: Formulário de contacto simples, que é o principal ponto de conversão da página.

Chat em Tempo Real: Widget de chat integrado usando Firebase Auth (autenticação anónima) e Cloud Firestore, permitindo comunicação direta com os visitantes.

Nickname Personalizado: Os utilizadores podem definir um nickname exclusivo, que é armazenado de forma privada no Firestore.

🛠️ Stack Tecnológico

Componente

Tecnologia

Propósito

Estrutura

HTML5 (ficheiro único)

Estrutura base da página.

Estilização

Tailwind CSS (CDN)

Estilização utilitária e responsiva.

Backend/DB

Google Firebase

Plataforma completa (Autenticação e Database).

Database

Cloud Firestore

Armazenamento persistente em tempo real para as mensagens do chat e perfis de utilizador.

Autenticação

Firebase Auth

Gerenciamento de sessões anónimas para o chat.

⚙️ Configuração e Implementação do Firebase

Para que o chat e o nickname funcionem, é fundamental garantir que o seu ambiente tem acesso às variáveis de configuração do Firebase e que as Regras de Segurança estão corretamente implementadas.

1. Variáveis de Configuração

O código depende das seguintes variáveis globais (fornecidas pelo ambiente de execução, como o Canvas):

\_\_firebase_config: Contém as credenciais do seu projeto Firebase (API Key, Project ID, etc.).

\_\_app_id: O ID do projeto/aplicação, usado para definir o caminho raiz no Firestore.

\_\_initial_auth_token: Token de autenticação inicial para iniciar a sessão.

2. Estrutura do Cloud Firestore

O código segue a convenção de segurança do Firebase para dados públicos e privados:

Tipo de Dado

Caminho do Firestore

Uso

Público

/artifacts/{appId}/public/data/chat_messages

Armazena todas as mensagens do chat (leitura/escrita permitida a utilizadores autenticados).

Privado

/artifacts/{appId}/users/{userId}/user_profile/profile

Armazena o nickname personalizado de cada utilizador (leitura/escrita permitida apenas ao próprio userId).

3. Regras de Segurança (FireStore Rules)

É obrigatório aplicar as seguintes regras no painel do Cloud Firestore (separador Regras na Consola do Firebase) para permitir o funcionamento e proteger os dados:

rules_version = '2';
service cloud.firestore {
match /databases/{database}/documents {
// Permite que utilizadores autenticados leiam e escrevam dados PÚBLICOS (chat)
match /artifacts/{appId}/public/data/{document=\*\*} {
allow read: if request.auth.uid != null;
allow write: if request.auth.uid != null;
}

    // Permite que um utilizador apenas leia e escreva os seus próprios dados PRIVADOS (nickname)
    match /artifacts/{appId}/users/{userId}/{document=**} {
      allow read, write: if request.auth.uid != null && request.auth.uid == userId;
    }

}
}

📝 Como Modificar e Ajustar

Cores e Estilo

As cores são definidas no bloco <script>...</script> do tailwind.config.

accent-teal: Cor primária de destaque (botões, títulos).

text-dark: Cor do texto.

hero-bg: O gradiente de fundo na secção principal pode ser ajustado no bloco <style>.

Textos e Conversão

Para otimizar a conversão da Landing Page:

Secção Hero (#inicio): Ajuste o título e o subtítulo para refletir a dor do seu cliente e a solução imediata que oferece.

Secção de Benefícios (#beneficios): Substitua os ícones (⚡️, ☁️, 🔒) e os textos para corresponderem aos seus principais diferenciais de serviço.

Chamada à Ação (#contacto): Garanta que o botão principal é a cor de destaque e que o texto inspira urgência ou valor.
