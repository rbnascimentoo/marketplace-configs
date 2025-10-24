# marketplace-configs

Repositório de configurações externas que serão servidas pelo Config Server para os microserviços do Marketplace.

## Estrutura

| Arquivo | Descrição |
| --- | --- |
| `application.yml` | Configurações compartilhadas (Eureka, observabilidade, Resilience4J, etc.). |
| `api-gateway*.yml` | Configurações da API Gateway (`api-gateway`) com perfis `dev` e `prod`. |
| `auth-service*.yml` | Configurações do serviço de autenticação (`auth-service`) com perfis `dev` e `prod`. |
| `config-server*.yml` | Configurações do Config Server com perfis `dev` e `prod`. |
| `notification-service*.yml` | Configurações do serviço de notificações com perfis `dev` e `prod`. |
| `order-service*.yml` | Configurações do serviço de pedidos com perfis `dev` e `prod`. |
| `payment-service*.yml` | Configurações do serviço de pagamentos com perfis `dev` e `prod`. |
| `product-service*.yml` | Configurações do serviço de produtos com perfis `dev` e `prod`. |
| `user-service*.yml` | Configurações do serviço de usuários com perfis `dev` e `prod`. |

Cada arquivo base (`*.yml`) é carregado automaticamente quando o microserviço com o mesmo `spring.application.name` solicita suas propriedades ao Config Server. Os arquivos com sufixo `-dev` e `-prod` utilizam `spring.config.activate.on-profile` para habilitar ajustes específicos por perfil de execução.

## Utilização

1. Configure o Config Server para apontar para este repositório.
2. Defina o `spring.application.name` em cada microserviço para que corresponda ao nome do arquivo desejado.
3. Ative o `spring.profiles.active` apropriado (`dev` ou `prod`) para carregar as propriedades adicionais do respectivo arquivo `*-{profile}.yml`.
4. Os segredos e endpoints sensíveis devem ser fornecidos via variáveis de ambiente conforme descrito nos placeholders (`${...}`) dentro dos arquivos.

## Boas práticas

- Não armazene segredos em texto plano. Utilize as variáveis de ambiente indicadas.
- Ajuste os valores padrão somente para cenários locais; ambientes remotos devem sobrescrever via variáveis ou cofre de segredos.
- Siga a mesma nomenclatura (`<service-name>`) ao adicionar novos microserviços para manter consistência.
