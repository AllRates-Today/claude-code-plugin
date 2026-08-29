# Covered sources

Every institution AllRatesToday ingests, with its API code and its dedicated npm
package. The code is what `/api/open/central-bank/{bank}`,
`/api/v1/central-bank/{bank}/...` and the MCP tools take as `bank`.

Coverage grows; `GET /api/v1/central-banks` (or the `list_central_banks` MCP
tool) is the live list and also carries each source's coverage window.

A per-source package pins one institution into a project without the rest of the
API surface — `npm install ecb-exchange-rate`, then call it like any client.
Docs per package: https://allratestoday.com/docs/sdk/<package>/

## Central banks (102)

| code | institution | country | home currency | npm |
|---|---|---|---|---|
| `boa` | Bank of Albania | Albania | ALL | `bank-of-albania-exchange-rate` |
| `bda` | Bank of Algeria | Algeria | DZD | `bank-of-algeria-exchange-rate` |
| `bna` | National Bank of Angola | Angola | AOA | `bna-exchange-rate` |
| `bcra` | Central Bank of Argentina | Argentina | ARS | `bcra-exchange-rate` |
| `cba` | Central Bank of Armenia | Armenia | AMD | `cba-exchange-rate` |
| `rba` | Reserve Bank of Australia | Australia | AUD | `rba-exchange-rate` |
| `cbar` | Central Bank of Azerbaijan | Azerbaijan | AZN | `cbar-exchange-rate` |
| `cbb` | Central Bank of Bahrain | Bahrain | BHD | `cbb-exchange-rate` |
| `bb` | Bangladesh Bank | Bangladesh | BDT | `bangladesh-bank-exchange-rate` |
| `nbrb` | National Bank of the Republic of Belarus | Belarus | BYN | `nbrb-exchange-rate` |
| `bcbol` | Banco Central de Bolivia | Bolivia | BOB | `banco-central-de-bolivia-exchange-rate` |
| `cbbh` | Central Bank of Bosnia and Herzegovina | Bosnia and Herzegovina | BAM | `cbbh-exchange-rate` |
| `bob` | Bank of Botswana | Botswana | BWP | `bob-exchange-rate` |
| `bcb` | Banco Central do Brasil (PTAX) | Brazil | BRL | `bcb-exchange-rate` |
| `bnb` | Bulgarian National Bank | Bulgaria | EUR | `bnb-exchange-rate` |
| `nbc` | National Bank of Cambodia | Cambodia | KHR | `nbc-cambodia-exchange-rate` |
| `boc` | Bank of Canada | Canada | CAD | `boc-exchange-rate` |
| `beac` | Bank of Central African States (BEAC) | Central Africa (CEMAC) | XAF | `beac-exchange-rate` |
| `bcch` | Central Bank of Chile | Chile | CLP | `central-bank-of-chile-exchange-rate` |
| `pboc` | People's Bank of China (CFETS) | China | CNY | `pboc-exchange-rate` |
| `sfc` | Superintendencia Financiera de Colombia (TRM) | Colombia | COP | `colombia-trm-exchange-rate` |
| `bccr` | Banco Central de Costa Rica | Costa Rica | CRC | `bccr-exchange-rate` |
| `cnb` | Czech National Bank | Czech Republic | CZK | `czech-national-bank-exchange-rate` |
| `dnb` | Danmarks Nationalbank | Denmark | DKK | `danmarks-nationalbank-exchange-rate` |
| `bcrd` | Banco Central de la República Dominicana | Dominican Republic | DOP | `bcrd-exchange-rate` |
| `cbe` | Central Bank of Egypt | Egypt | EGP | `cbe-exchange-rate` |
| `nbe` | National Bank of Ethiopia | Ethiopia | ETB | `national-bank-of-ethiopia-exchange-rate` |
| `ecb` | European Central Bank | Eurozone | EUR | `ecb-exchange-rate` |
| `nbg` | National Bank of Georgia | Georgia | GEL | `nbg-exchange-rate` |
| `bog` | Bank of Ghana | Ghana | GHS | `bank-of-ghana-exchange-rate` |
| `banguat` | Banco de Guatemala | Guatemala | GTQ | `banguat-exchange-rate` |
| `bogy` | Bank of Guyana | Guyana | GYD | `bank-of-guyana-exchange-rate` |
| `bch` | Banco Central de Honduras | Honduras | HNL | `bch-exchange-rate` |
| `hkma` | Hong Kong Monetary Authority | Hong Kong | HKD | `hkma-exchange-rate` |
| `mnb` | Magyar Nemzeti Bank | Hungary | HUF | `magyar-nemzeti-bank-exchange-rate` |
| `cbi` | Central Bank of Iceland | Iceland | ISK | `central-bank-of-iceland-exchange-rate` |
| `rbi` | Reserve Bank of India | India | INR | `rbi-exchange-rate` |
| `bi` | Bank Indonesia | Indonesia | IDR | `bank-indonesia-exchange-rate` |
| `cbiq` | Central Bank of Iraq | Iraq | IQD | `central-bank-of-iraq-exchange-rate` |
| `boi` | Bank of Israel | Israel | ILS | `bank-of-israel-exchange-rate` |
| `bdi` | Banca d'Italia | Italy | EUR | `bdi-exchange-rate` |
| `bojm` | Bank of Jamaica | Jamaica | JMD | `bank-of-jamaica-exchange-rate` |
| `boj` | Bank of Japan | Japan | JPY | `boj-exchange-rate` |
| `cbj` | Central Bank of Jordan | Jordan | JOD | `cbj-exchange-rate` |
| `nbk` | National Bank of Kazakhstan | Kazakhstan | KZT | `nbk-exchange-rate` |
| `cbke` | Central Bank of Kenya | Kenya | KES | `central-bank-of-kenya-exchange-rate` |
| `cbk` | Central Bank of Kuwait | Kuwait | KWD | `cbk-exchange-rate` |
| `nbkr` | National Bank of the Kyrgyz Republic | Kyrgyzstan | KGS | `nbkr-exchange-rate` |
| `bol` | Bank of the Lao PDR | Laos | LAK | `bank-of-laos-exchange-rate` |
| `amcm` | Monetary Authority of Macao | Macao | MOP | `amcm-exchange-rate` |
| `rbm` | Reserve Bank of Malawi | Malawi | MWK | `rbm-exchange-rate` |
| `bnm` | Bank Negara Malaysia | Malaysia | MYR | `bnm-exchange-rate` |
| `bmu` | Bank of Mauritius | Mauritius | MUR | `bmu-exchange-rate` |
| `banxico` | Banco de México | Mexico | MXN | `banxico-exchange-rate` |
| `nbm` | National Bank of Moldova | Moldova | MDL | `nbm-exchange-rate` |
| `bom` | Bank of Mongolia | Mongolia | MNT | `bank-of-mongolia-exchange-rate` |
| `bam` | Bank Al-Maghrib | Morocco | MAD | `bank-al-maghrib-exchange-rate` |
| `bdm` | Banco de Moçambique | Mozambique | MZN | `bdm-exchange-rate` |
| `cbm` | Central Bank of Myanmar | Myanmar | MMK | `cbm-exchange-rate` |
| `nrb` | Nepal Rastra Bank | Nepal | NPR | `nrb-exchange-rate` |
| `rbnz` | Reserve Bank of New Zealand | New Zealand | NZD | `rbnz-exchange-rate` |
| `bcn` | Banco Central de Nicaragua | Nicaragua | NIO | `bcn-exchange-rate` |
| `cbn` | Central Bank of Nigeria | Nigeria | NGN | `cbn-exchange-rate` |
| `nbrm` | National Bank of North Macedonia | North Macedonia | MKD | `nbrm-exchange-rate` |
| `norges` | Norges Bank | Norway | NOK | `norges-bank-exchange-rate` |
| `cbo` | Central Bank of Oman | Oman | OMR | `cbo-exchange-rate` |
| `sbp` | State Bank of Pakistan | Pakistan | PKR | `sbp-exchange-rate` |
| `pma` | Palestine Monetary Authority | Palestine | ILS | `palestine-monetary-authority-exchange-rate` |
| `bcp` | Banco Central del Paraguay | Paraguay | PYG | `bcp-exchange-rate` |
| `bcrp` | Central Reserve Bank of Peru | Peru | PEN | `bcrp-exchange-rate` |
| `bsp` | Bangko Sentral ng Pilipinas | Philippines | PHP | `bsp-exchange-rate` |
| `nbp` | Narodowy Bank Polski | Poland | PLN | `nbp-exchange-rate` |
| `qcb` | Qatar Central Bank | Qatar | QAR | `qcb-exchange-rate` |
| `bnr` | National Bank of Romania | Romania | RON | `bnr-exchange-rate` |
| `cbr` | Bank of Russia | Russia | RUB | `cbr-exchange-rate` |
| `bnrw` | National Bank of Rwanda | Rwanda | RWF | `national-bank-of-rwanda-exchange-rate` |
| `sama` | Saudi Central Bank (SAMA) | Saudi Arabia | SAR | `sama-exchange-rate` |
| `nbs` | National Bank of Serbia | Serbia | RSD | `national-bank-of-serbia-exchange-rate` |
| `mas` | Monetary Authority of Singapore | Singapore | SGD | `mas-exchange-rate` |
| `sarb` | South African Reserve Bank | South Africa | ZAR | `sarb-exchange-rate` |
| `bok` | Bank of Korea | South Korea | KRW | `bok-exchange-rate` |
| `cbsl` | Central Bank of Sri Lanka | Sri Lanka | LKR | `cbsl-exchange-rate` |
| `cbvs` | Central Bank of Suriname | Suriname | SRD | `central-bank-of-suriname-exchange-rate` |
| `riksbank` | Sveriges Riksbank | Sweden | SEK | `riksbank-exchange-rate` |
| `snb` | Swiss National Bank | Switzerland | CHF | `snb-exchange-rate` |
| `cbc` | Central Bank of the Republic of China (Taiwan) | Taiwan | TWD | `taiwan-central-bank-exchange-rate` |
| `botz` | Bank of Tanzania | Tanzania | TZS | `bank-of-tanzania-exchange-rate` |
| `bot` | Bank of Thailand | Thailand | THB | `bank-of-thailand-exchange-rate` |
| `cbtt` | Central Bank of Trinidad and Tobago | Trinidad and Tobago | TTD | `cbtt-exchange-rate` |
| `bct` | Central Bank of Tunisia | Tunisia | TND | `bct-exchange-rate` |
| `tcmb` | Central Bank of Türkiye | Türkiye | TRY | `tcmb-exchange-rate` |
| `bou` | Bank of Uganda | Uganda | UGX | `bou-exchange-rate` |
| `nbu` | National Bank of Ukraine | Ukraine | UAH | `nbu-exchange-rate` |
| `cbuae` | Central Bank of the UAE | United Arab Emirates | AED | `cbuae-exchange-rate` |
| `boe` | Bank of England | United Kingdom | GBP | `boe-exchange-rate` |
| `fed` | US Federal Reserve (H.10) | United States | USD | `fed-exchange-rate` |
| `bcu` | Central Bank of Uruguay | Uruguay | UYU | `bcu-exchange-rate` |
| `cbu` | Central Bank of Uzbekistan | Uzbekistan | UZS | `cbu-exchange-rate` |
| `bcv` | Central Bank of Venezuela | Venezuela | VES | `central-bank-of-venezuela-exchange-rate` |
| `sbv` | State Bank of Vietnam | Vietnam | VND | `sbv-exchange-rate` |
| `bceao` | Central Bank of West African States (BCEAO) | West Africa (WAEMU) | XOF | `bceao-exchange-rate` |
| `boz` | Bank of Zambia | Zambia | ZMW | `boz-exchange-rate` |

## Tax & customs authorities (3)

| code | institution | country | home currency | npm |
|---|---|---|---|---|
| `bazg` | Swiss Federal Office for Customs and Border Security | Switzerland | CHF | `bazg-exchange-rate` |
| `hmrc` | HM Revenue & Customs | United Kingdom | GBP | `hmrc-exchange-rate` |
| `ustreasury` | U.S. Department of the Treasury | United States | USD | `ustreasury-exchange-rate` |

## Composite (1)

| code | institution | country | home currency | npm |
|---|---|---|---|---|
| `composite` | Composite Official Rate | Global | USD | — |
