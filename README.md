# Diário Motor - Parkinson

Aplicação web para monitoramento contínuo do estado clínico de pacientes com Doença de Parkinson, permitindo registro automático e manual das flutuações motoras ao longo do dia.

## 📋 Descrição

O **Diário Motor** é uma ferramenta digital desenvolvida para auxiliar pacientes com Doença de Parkinson e seus médicos no acompanhamento das flutuações motoras (fenômenos ON-OFF e discinesias). A aplicação solicita avaliações periódicas do estado clínico do paciente, gerando relatórios detalhados que podem ser compartilhados com a equipe médica.

## ✨ Funcionalidades Principais

### 🔔 Sistema de Alarmes Automatizados
- Lembretes sonoros e visuais a cada 30 minutos (configurável)
- Notificações push do navegador
- Avaliação basal ao acordar
- Registro manual disponível a qualquer momento

### 📊 Registro de Estados Clínicos
- **ON (Bem)**: Mobilidade boa, medicação funcionando adequadamente
- **ON com Discinesia (DYS)**: Movimentos involuntários presentes
- **OFF (Travado)**: Rigidez, lentidão ou imobilidade

### 📈 Visualização e Análise
- Lista cronológica de todas as avaliações do dia
- Resumo estatístico (contagem e percentual de cada estado)
- Indicador do próximo horário de avaliação

### 📤 Exportação de Dados
- **CSV**: Para análise em planilhas
- **JSON**: Para integração com outros sistemas
- **PDF**: Relatório formatado para impressão
- **E-mail**: Envio automático ao médico via EmailJS

### 💾 Armazenamento Local
- Dados salvos no navegador (LocalStorage)
- Não requer conexão constante com a internet
- Sessões podem ser finalizadas e reiniciadas

## 🚀 Como Usar

### 1. Configuração Inicial

Abra o arquivo `index.html` em um navegador web moderno (Chrome, Firefox, Safari, Edge).

### 2. Cadastro do Paciente

Preencha as seguintes informações:
- Nome completo
- CPF (com formatação automática)
- E-mail do médico para receber o relatório

### 3. Início do Monitoramento

- Permita notificações quando solicitado
- A primeira avaliação (basal) será solicitada imediatamente
- A partir daí, alarmes soarão a cada 30 minutos

### 4. Durante o Dia

- Responda a cada alarme informando seu estado atual
- Use o botão "Registrar Avaliação Agora" para registros manuais
- Acompanhe suas avaliações na aba "Diário"

### 5. Finalização

- Ao final do dia, clique em "Finalizar Dia (Ir Dormir)"
- Revise o resumo estatístico
- Envie o relatório por e-mail ou baixe os arquivos localmente

## 🔧 Configuração do EmailJS

Para habilitar o envio automático de e-mails, configure o EmailJS:

### Passo 1: Criar Conta no EmailJS
1. Acesse [emailjs.com](https://www.emailjs.com/)
2. Crie uma conta gratuita
3. Configure um serviço de e-mail (Gmail, Outlook, etc.)

### Passo 2: Criar Template de E-mail
Crie um template com os seguintes parâmetros:
- `to_email`: E-mail de destino
- `patient_name`: Nome do paciente
- `patient_cpf`: CPF do paciente
- `date`: Data do relatório
- `total_evaluations`: Total de avaliações
- `csv_content`: Anexo CSV (base64)
- `json_content`: Anexo JSON (base64)
- `pdf_content`: Anexo PDF (base64)

### Passo 3: Atualizar as Credenciais

No arquivo HTML, localize a seção `EMAILJS_CONFIG` e substitua pelos seus valores:

```javascript
const EMAILJS_CONFIG = {
    publicKey: 'SUA_PUBLIC_KEY',      // Da sua conta EmailJS
    serviceId: 'SEU_SERVICE_ID',      // ID do serviço configurado
    templateId: 'SEU_TEMPLATE_ID'     // ID do template criado
};
```

### Passo 4: Descomentar Inicialização

Descomente a linha de inicialização do EmailJS:

```javascript
emailjs.init(EMAILJS_CONFIG.publicKey);
```

## 💻 Tecnologias Utilizadas

### Front-end
- **HTML5**: Estrutura semântica
- **CSS3**: Estilização responsiva com variáveis CSS e animações
- **JavaScript ES6+**: Lógica da aplicação

### Bibliotecas Externas
- **jsPDF** (v2.5.1): Geração de arquivos PDF
- **jsPDF AutoTable** (v3.5.29): Criação de tabelas em PDF
- **EmailJS** (v3): Envio de e-mails sem back-end

### APIs do Navegador
- **LocalStorage API**: Persistência de dados
- **Notification API**: Notificações push
- **Wake Lock API**: Manter tela ativa (quando disponível)
- **Audio API**: Reprodução de alarmes sonoros

## 📁 Estrutura de Dados

### Formato de Avaliação
```json
{
  "timestamp": "2025-02-04T14:30:00.000Z",
  "timeFormatted": "14:30",
  "dateFormatted": "04/02/2025",
  "status": "ON",
  "type": "regular"
}
```

### Estados Possíveis
- `status`: `"ON"`, `"DYS"`, ou `"OFF"`
- `type`: `"basal"`, `"regular"`, ou `"manual"`

### Arquivo CSV Exportado
```csv
Nome,CPF,Data,Hora,Timestamp,Status,Status_Codigo,Tipo_Avaliacao
"João Silva","123.456.789-00","04/02/2025","08:00","2025-02-04T08:00:00.000Z","ON",2,"basal"
```

**Códigos de Status:**
- `1`: OFF
- `2`: ON
- `3`: DYS (Discinesia)

## ⚙️ Configurações Disponíveis

### Intervalo entre Avaliações
- Padrão: 30 minutos
- Configurável entre 5 e 120 minutos
- Acessível na aba "Config"

### E-mail de Destino
- Pode ser alterado a qualquer momento
- Usado para envio do relatório final

### Reset de Dados
- Opção para apagar todos os dados armazenados
- Útil para iniciar novo período de monitoramento

## 🔒 Privacidade e Segurança

- **Armazenamento Local**: Todos os dados ficam no navegador do paciente
- **Sem Servidor**: Não há envio de dados para servidores terceiros (exceto via EmailJS configurado)
- **Controle Total**: O paciente controla quando e para quem enviar os dados
- **LGPD Compliant**: Adequado à Lei Geral de Proteção de Dados

## 📱 Compatibilidade

### Navegadores Suportados
- ✅ Chrome/Edge (recomendado)
- ✅ Firefox
- ✅ Safari
- ⚠️ Navegadores móveis (funcionalidade limitada de notificações)

### Requisitos
- JavaScript habilitado
- Permissão para notificações (opcional, mas recomendado)
- Armazenamento local disponível

## 🎯 Casos de Uso Clínico

### Ajuste de Medicação
Os dados permitem ao médico:
- Identificar períodos de OFF prolongados
- Detectar discinesias relacionadas aos picos de medicação
- Otimizar horários e doses dos medicamentos

### Pesquisa Clínica
- Endpoint objetivo para estudos de intervenção
- Dados estruturados para análise estatística
- Formato compatível com softwares de pesquisa (R, Python, SPSS)

### Telemedicina
- Envio de relatórios entre consultas
- Acompanhamento remoto do estado clínico
- Documentação objetiva para teleconsultas

## 🚧 Limitações Conhecidas

1. **Alarmes em Segundo Plano**: Navegadores móveis podem suspender alarmes quando o app está inativo
2. **Notificações**: Requerem permissão do usuário e podem não funcionar em todos os dispositivos
3. **HTTPS**: Algumas funcionalidades (Wake Lock, Service Workers) requerem HTTPS em produção
4. **EmailJS**: Serviço gratuito tem limite mensal de envios

## 🔮 Desenvolvimentos Futuros

- [ ] Progressive Web App (PWA) para instalação no celular
- [ ] Sincronização em nuvem
- [ ] Gráficos de tendência temporal
- [ ] Integração com smartwatches
- [ ] Modo offline completo com Service Worker
- [ ] Exportação para formato FHIR (padrão de interoperabilidade em saúde)

## 📄 Licença

Este projeto é disponibilizado para uso educacional e clínico. Para uso comercial ou em pesquisa, favor entrar em contato com os desenvolvedores.

## 👨‍⚕️ Autoria

Desenvolvido para uso em neurologia clínica com foco em transtornos do movimento.

## 🤝 Contribuições

Sugestões e melhorias são bem-vindas! Para contribuir:

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abra um Pull Request

## 📞 Suporte

Para questões técnicas ou sugestões de melhorias, abra uma issue no repositório.

## ⚠️ Disclaimer Médico

Esta aplicação é uma ferramenta de auxílio diagnóstico e monitoramento. Não substitui a avaliação clínica presencial e o julgamento médico especializado. Sempre consulte um neurologista para interpretação dos dados e ajustes terapêuticos.

---

**Versão**: 2.0  
**Última Atualização**: Fevereiro 2025
