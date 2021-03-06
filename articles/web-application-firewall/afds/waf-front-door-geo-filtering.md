---
title: Filtragem geográfica em um domínio do Azure Front Door
description: Neste artigo, você aprenderá sobre a política de filtragem geográfica do Azure Front Door Service
services: web-application-firewall
author: vhorne
ms.service: web-application-firewall
ms.topic: conceptual
ms.date: 03/10/2020
ms.author: victorh
ms.reviewer: tyao
ms.openlocfilehash: fcd7a0fe60639bbb17661a906d15136996b325e4
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87005439"
---
# <a name="what-is-geo-filtering-on-a-domain-for-azure-front-door-service"></a>O que é filtragem geográfica em um domínio para o serviço de porta frontal do Azure?

Por padrão, o Azure Front Door Service responde às solicitações de usuário, independentemente do local do usuário que faz a solicitação. No entanto, em alguns casos, é possível restringir o acesso ao conteúdo dos aplicativos Web por país/região. O serviço WAF (firewall do aplicativo Web) no Front Door permite que você defina uma política usando regras personalizadas de acesso para um caminho específico no seu ponto de extremidade para permitir ou bloquear o acesso de países/regiões específicos. 

Uma política de WAF geralmente inclui um conjunto de regras personalizadas. Uma regra é composta de condições de correspondência, uma ação e uma prioridade. Na condição de correspondência, você define uma variável de correspondência, operador e valor de correspondência.  Para a regra de filtragem geográfica, a variável de correspondência é REMOTE_ADDR, o operador é GeoMatch, o valor é o código de interesse do país/região de duas letras. Você pode combinar uma condição GeoMatch e uma condição de correspondência de cadeia de caracteres REQUEST_URI para criar uma regra de filtragem geográfica com base no caminho.

Você pode configurar uma política de filtragem geográfica para seu Front Door usando o [Azure PowerShell](waf-front-door-tutorial-geo-filtering.md) ou usando nosso [modelo de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/101-front-door-geo-filtering).

## <a name="countryregion-code-reference"></a>Referência de código de país/região

|Código de país/região | Nome de país/região |
| ----- | ----- |
| AD | Andorra |
| AE | Emirados Árabes Unidos|
| AF | Afeganistão|
| AG | Antígua e Barbuda|
| AL | Albânia|
| AM | Armênia|
| AO | Angola|
| AR | Argentina|
| AS | Samoa Americana|
| AT | Áustria|
| AU | Austrália|
| AZ | Azerbaijão|
| BA | Bósnia e Herzegovina|
| BB | Barbados|
| BD | Bangladesh|
| BE | Bélgica|
| BF | Burkina Faso|
| BG | Bulgária|
| BH | Bahrein|
| BI | Burundi|
| BJ | Benin|
| BL | São Bartolomeu|
| BN | Brunei Darussalam|
| BO | Bolívia|
| BR | Brasil|
| BS | Bahamas|
| BT | Butão|
| BW | Botsuana|
| BY | Belarus|
| BZ | Belize|
| CA | Canada|
| CD | República Democrática do Congo|
| CF | República Centro-Africana|
| CH | Suíça|
| CI | Costa do Marfim|
| CL | Chile|
| CM | Camarões|
| CN | China|
| CO | Colômbia|
| CR | Costa Rica|
| CU | Cuba|
| CV | Cabo Verde|
| CY | Chipre|
| CZ | República Tcheca|
| DE | Alemanha|
| DK | Dinamarca|
| DO | República Dominicana|
| DZ | Argélia|
| EC | Equador|
| EE | Estônia|
| EG | Egito|
| ES | Espanha|
| ET | Etiópia|
| FI | Finlândia|
| FJ | Fiji|
| FM | Micronésia, Estados Federados da|
| FR | França|
| GB | United Kingdom|
| GE | Geórgia|
| GF | Guiana Francesa|
| GH | Gana|
| GN | Guiné|
| GP | Guadalupe|
| GR | Grécia|
| GT | Guatemala|
| GY | Guiana|
| HK | RAE de Hong Kong|
| HN | Honduras|
| HR | Croácia|
| HT | Haiti|
| HU | Hungria|
| ID | Indonésia|
| IE | Irlanda|
| IL | Israel|
| IN | Índia|
| IQ | Iraque|
| IR | Irã, República Islâmica do|
| IS | Islândia|
| IT | Itália|
| JM | Jamaica|
| JO | Jordânia|
| JP | Japão|
| KE | Quênia|
| KG | Quirguistão|
| KH | Camboja|
| KI | Kiribati|
| KN | São Cristóvão e Névis|
| KP | Coreia, República Democrática Popular da|
| KR | Coreia, República da|
| KW | Kuwait|
| KY | Ilhas Cayman|
| KZ | Cazaquistão|
| LA | República Democrática do Laos|
| LB | Líbano|
| LI | Liechtenstein|
| LK | Sri Lanka|
| LR | Libéria|
| LS | Lesoto|
| LT | Lituânia|
| LU | Luxemburgo|
| LV | Letônia|
| LY | Líbia |
| MA | Marrocos|
| MD | Moldávia, República da|
| MG | Madagascar|
| MK | Macedônia do Norte|
| ML | Mali|
| MM | Myanmar|
| MN | Mongólia|
| MO | RAE de Macau|
| MQ | Martinica|
| MR | Mauritânia|
| MT | Malta|
| MV | Maldivas|
| MW | Malaui|
| MX | México|
| MY | Malásia|
| MZ | Moçambique|
| NA | Namíbia|
| NE | Níger|
| NG | Nigéria|
| NI | Nicarágua|
| NL | Países Baixos|
| Não | Noruega|
| NP | Nepal|
| NR | Nauru|
| NZ | Nova Zelândia|
| OM | Omã|
| PA | Panamá|
| PE | Peru|
| PH | Filipinas|
| PK | Paquistão|
| PL | Polônia|
| PR | Porto Rico|
| PT | Portugal|
| PW | Palau|
| PY | Paraguai|
| QA | Catar|
| RE | Reunião|
| RO | Romênia|
| RS | Sérvia|
| RU | Federação Russa|
| RW | Ruanda|
| SA | Arábia Saudita|
| SD | Sudão|
| SE | Suécia|
| SG | Singapura|
| SI | Eslovênia|
| SK | Eslováquia|
| SN | Senegal|
| SO | Somália|
| SR | Suriname|
| SS | Sudão do Sul|
| SV | El Salvador|
| SY | República Árabe Síria|
| SZ | Suazilândia|
| TC | Ilhas Turcas e Caicos|
| TG | Togo|
| TH | Tailândia|
| TN | Tunísia|
| TR | Turquia|
| TT | Trinidad e Tobago|
| TW | Taiwan|
| TZ | Tanzânia, República Unida da|
| UA | Ucrânia|
| UG | Uganda|
| EUA | Estados Unidos|
| UY | Uruguai|
| UZ | Uzbequistão|
| VC | São Vincent e Granadinas|
| VE | Venezuela|
| VG | Ilhas Virgens Britânicas|
| VI | Ilhas Virgens Americanas|
| VN | Vietnã|
| ZA | África do Sul|
| ZM | Zâmbia|
| ZW | Zimbábue|

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [segurança da camada de aplicativo com o Front Door](../../frontdoor/front-door-application-security.md).
- Saiba como [criar um Front Door](../../frontdoor/quickstart-create-front-door.md).
