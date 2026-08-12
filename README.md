# 🎧 Mapeando os Bastidores da Web: Anatomia de uma API (Spotify Web)

**Desenvolvedor:** Jheyson Siqueira  
**Tecnologias Analisadas:** Protocolo HTTP/HTTPS, APIs RESTful e GraphQL, JSON, Google Chrome DevTools, Diagramação estrutural.

## 1. Resumo do Projeto
Este projeto é um estudo de engenharia reversa e análise arquitetural da comunicação web moderna, utilizando o **Spotify Web Player** como objeto de estudo. Através da interceptação de rede, foi possível documentar o ciclo de vida das requisições HTTP, a semântica dos métodos e a estruturação de payloads em JSON em uma arquitetura Single Page Application (SPA).

## 2. Endpoints e Mapeamento de Tráfego HTTP

Durante a auditoria de rede, as seguintes requisições foram inspecionadas:

| Método | Endpoint Inspecionado | Função na Aplicação | Status |
| :--- | :--- | :--- | :--- |
| `GET` | `/v1/me/player/currently-playing` | Obter dados da faixa em reprodução. | `200 OK` |
| `POST` | `/pathfinder/v2/query` | Busca dinâmica (GraphQL) no catálogo. | `200 OK` |
| `POST` | `/v1/users/me/playlists` | Criar nova playlist. | `201 Created` |
| `PUT` | `/v1/me/player/play` | Enviar comando de controle (play/resume). | `204 No Content` |
| `DELETE` | `/v1/me/tracks?ids=...` | Remover música das "Curtidas". | `200 OK` |

## 3. Evidências Práticas (DevTools)

Abaixo estão as capturas de rede comprovando a auditoria dos dados trafegados:

### Captura de Requisição GET
![Evidência GET](Evidência%2001%20-%20Captura%20de%20Requisição%20GET%20(Status%20200)%20-%20Spotify.jpeg)

### Captura de API (GraphQL Query)
![Evidência POST](Evidência%2002%20-%20Captura%20de%20API%20Fetch_XHR%20(GraphQL%20Query)%20-%20Spotify.jpeg)

## 4. Fluxograma de Comunicação Cliente-Servidor

O diagrama abaixo representa visualmente o ciclo de vida de uma consulta complexa de busca (POST em ambiente GraphQL) dentro do Spotify:

![Fluxograma de Comunicação](fluxograma_comunicacao_spotify.jpg)

## 5. Parecer Técnico Consolidado
A análise comprovou a eficiência de três pilares fundamentais no back-end do Spotify:
* **Requisições Desacopladas (Fetch API):** Garantem economia de banda e fluidez na interface React.
* **Uso Estratégico de CDNs:** Separam os ativos estáticos pesados dos endpoints de regras de negócios.
* **Padronização JSON e Comunicação Stateless:** Uso de Bearer Tokens para validar identidades de forma segura e distribuída.
