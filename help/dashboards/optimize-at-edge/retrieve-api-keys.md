---
title: Recupere suas chaves de API
description: Como recuperar suas chaves de API de produção e de preparo da otimização na borda no LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:58:10.897Z'
TQID: 'https://experienceleague.adobe.com/4R-cx6wv75Oowj9ZvEPGCzQbQBSoppgDuI5Ut1IbObA'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 100%

---


# Recupere suas chaves de API

Antes de configurar a CDN, recupere as chaves de API da otimização na borda na interface do usuário do LLM Optimizer. Você precisa de uma chave de API de **produção** para tráfego real. Opcionalmente, você também pode recuperar uma chave de API de **preparo** para testar o roteamento em um nome de host de preparo primeiro.

## Chave da API de produção

1. No LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.

   ![Acesse a configuração do cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Localize a seção **Implantar otimizações em agentes de IA**. Marque a caixa de seleção **Habilitar mecanismo de otimização**.

   ![Implantar otimizações nos agentes de IA — pendente](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. Na caixa de diálogo de confirmação, selecione **Habilitar**.

   ![Habilitar caixa de diálogo de confirmação do mecanismo de otimização](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. Selecione **Visualizar detalhes**. Na caixa de diálogo **Detalhes da implantação das otimizações**, copie a **chave de API de produção** (use **Copiar** ao lado do campo).

   ![Chave de API de produção nos detalhes da implantação das otimizações](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >A caixa de diálogo pode indicar que a configuração não foi concluída. Isso é esperado até que o roteamento seja verificado — você ainda pode copiar a chave da API para que sua equipe de TI ou de CDN possa concluir a configuração.

Se você precisar de ajuda com as etapas acima, entre em contato com a equipe de contas da Adobe ou com `llmo-at-edge@adobe.com`.

## Chave de API de preparo (opcional)

Para validar o roteamento em um ambiente inferior antes de habilitar o roteamento de produção, você pode configurar um nome de host de preparo.

**Requisitos**

* O nome do host de preparo deve estar no **mesmo domínio registrável** que o de produção (por exemplo, `https://staging.example.com` quando a produção for `https://www.example.com`).
* Apenas **um** domínio de preparo por site. Depois de salvo, ele não pode ser alterado sem entrar em contato com a Adobe.

**Etapas**

1. No LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.
2. Em **Implantar otimizações em agentes de IA**, selecione **Adicionar domínio de preparo** (ou **Domínio de preparo** se um domínio de preparo já estiver configurado).
3. Insira o URL de preparo completo, incluindo `https://`, e selecione **Definir domínio**.
4. Copie a chave de API de **preparo** da caixa de diálogo de confirmação.

   ![Chave de API do domínio de preparo](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Implante as mesmas regras de roteamento em seu ambiente de preparo usando a chave de API de preparo.

Se precisar de ajuda, entre em contato com `llmo-at-edge@adobe.com`.

## Próximas etapas

Após recuperar suas chaves de API, retorne ao [guia de configuração da CDN](/help/dashboards/optimize-at-edge/overview.md#cdn-configuration-guides) para configurar o roteamento.
