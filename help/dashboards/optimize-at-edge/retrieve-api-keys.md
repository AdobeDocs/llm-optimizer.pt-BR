---
title: Recuperar suas chaves de API
description: Como recuperar as chaves de API de otimização para Edge de produção e preparo do LLM Optimizer.
feature: Opportunities
source-git-commit: 3b6dc163f4488a22937916beb6778de4abc5a20c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Recuperar suas chaves de API

Antes de configurar o CDN, recupere as chaves da API Otimizada do Edge na interface do usuário do LLM Optimizer. Você precisa de uma chave de API de **produção** para o tráfego direto. Como opção, você também pode recuperar uma chave de API de **preparo** para testar primeiro o roteamento em um nome de host de preparo.

## Chave da API de produção

1. Na LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Localize a seção **Implantar otimizações em agentes de IA**. Marque a caixa de seleção **Habilitar mecanismo de otimização**.

   ![Implantar otimizações em agentes de IA — pendente](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. No diálogo de confirmação, selecione **Habilitar**.

   ![Habilitar caixa de diálogo de confirmação do mecanismo de otimização](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. Selecione **Exibir detalhes**. Na caixa de diálogo **Implantar detalhes de otimizações**, copie a **Chave da API de Produção** (use **Copiar** ao lado do campo).

   ![Chave da API de produção em Detalhes de otimizações de implantação](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >A caixa de diálogo pode mostrar que a configuração não está concluída. Isso é esperado até que o roteamento seja verificado — você ainda pode copiar a chave da API para que sua equipe de TI ou de CDN possa concluir a configuração.

Se você precisar de ajuda com as etapas acima, contate a equipe de conta da Adobe ou o `llmo-at-edge@adobe.com`.

## Chave da API de preparo (opcional)

Para validar o roteamento em um ambiente inferior antes de habilitar o roteamento de produção, você pode configurar um nome de host de preparo.

**Requisitos**

* O nome de host de preparo deve estar no **mesmo domínio registrável** que a produção (por exemplo, `https://staging.example.com` quando a produção for `https://www.example.com`).
* Apenas **um** domínio de preparo por site. Depois de salvo, não é possível alterá-lo sem entrar em contato com a Adobe.

**Etapas**

1. Na LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.
2. Em **Implantar otimizações para agentes de IA**, selecione **Adicionar domínio de preparo** (ou **Domínio de preparo** se um domínio de preparo já estiver configurado).
3. Insira a URL de preparo completa incluindo `https://` e selecione **Definir Domínio**.
4. Copie a chave de API de **preparo** da caixa de diálogo de confirmação.

   ![Chave de API do domínio de preparo](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Implante as mesmas regras de roteamento no ambiente de preparo usando a chave de API de preparo.

Se precisar de ajuda, contate `llmo-at-edge@adobe.com`.

## Próximas etapas

Depois de recuperar as chaves de API, retorne ao [guia de instalação do CDN](/help/dashboards/optimize-at-edge/overview.md#cdn-configuration-guides) para configurar o roteamento.
