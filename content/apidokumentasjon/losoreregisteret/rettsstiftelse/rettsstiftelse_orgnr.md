---
title: Henting av rettsstiftelser knyttet til virksomhet
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 130
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                       | Beskrivelse                                                              |
|:------------- |:----------------------------------------------------------|:-------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v1/rettsstiftelse/orgnr/\{orgnr}\?sluttbrukerOrgNr={sluttbrukerOrgNr}  | Hent opplysninger om rettstiftelser knyttet til et organisasjonsnummer. SluttbrukerOrgNr er valgfri  |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive rettstiftelser på organisasjonsnummer.

#### Request

Tar i mot et organisasjonsnummer (orgnr) som del av URL.
Valgfri parameter "sluttbrukerOrgNr" muliggjør at konsumenten kan presisere at oppslaget gjøres på vegne av en tredjepart som har avtale med konsumenten om uthenting av data. Dette er mest aktuelt for avtaleparter som omtales som distributører. Parameteren forventes utformet som et standard organisasjonsnummer fra Enhetsregisteret.

#### Validering av forespørsler

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig samt ha en gyldig avtale om å kunne hente ut opplysninger i Løsøreregisteret.
* Forespørselen skal alltid inneholde orgnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et orgnr som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Dersom forespørselen inneholder parameter "sluttbrukerOrgNr" som ikke er lovlig oppbygd, returneres det en feilmelding

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
    "sokeparameter": "810843012",
    "oppslagstidspunkt": "2020-10-28T12:44:43.479",
    "antallRettsstiftelser": 3,
    "rettsstiftelser": [
        {
            "dokumentnummer": "2020000167",
            "type": "rettsstiftelsestype.utp",
            "typeBeskrivelse": "Utleggspant",
            "innkomsttidspunkt": "2016-09-22T15:49:58.023",
            "ajourtidspunkt": "2020-05-26T12:10:14.705",
            "status": "statusregistreringsobjekt.tl",
            "statusBeskrivelse": "tinglyst",
            "beslutningstidspunkt": "2020-02-10T09:02:00",
            "roller": [
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.namsmyndighet",
                    "rolletypeBeskrivelse": "Namsmyndighet",
                    "navn": "ENGSTELIG TIGER AS",
                    "forretningsadresse": {
                        "adresse": [ "Stjørdal 123" ],
                        "poststed": "Stjørdal",
                        "postnummer": "7504",
                        "kommune": "Stjørdal",
                        "kommunenummer": "2345",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810843012
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",                    
                    "navn": "ENORM TIGER AS",
                    "forretningsadresse": {
                        "adresse": [ "Ålesundgata 123" ],
                        "poststed": "Ålesund",
                        "postnummer": "6011",
                        "kommune": "Ålesund",
                        "kommunenummer": "1234",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810843942
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "LYDIG IDYLL"
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "BRITISH TIGER AS",
                    "forretningsadresse": {
                        "adresse": [ "123 Tiger Street" ],
                        "poststed": "London 456",
                        "land": "Storbritania",
                        "landkode": "GB"
                    },
                    "orgnr": 810738952
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "BLÅ KATT DUEHISTOLOG",
                    "forretningsadresse": {
                        "adresse": [ "Drammensgata 123" ],
                        "poststed": "Drammen",
                        "postnummer": "3044",
                        "kommune": "Drammen",
                        "kommunenummer": "3456",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810864192
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksoker",
                    "rolletypeBeskrivelse": "Saksøker",
                    "navn": "OPPLAGT KUNNSKAP",
                    "adresse": "Kulsrudgutua 2C"
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksoker",
                    "rolletypeBeskrivelse": "Saksøker",
                    "navn": "INNSIKTSFULL BIE"
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksokt",
                    "rolletypeBeskrivelse": "Saksøkt",
                    "navn": "Annie Andersson"
                }
            ],
            "formuesgoder": [
                {
                    "type": "formuesgodetype.mv.e",
                    "typeBeskrivelse": "motorvogn registrert",
                    "identifiseringsmaateFormuesgode": {
                        "registreringsnummerMotorvogn": "CU10102"
                    },
                    "eierandel": {
                        "teller": 1,
                        "nevner": 1
                    }
                },
                {
                    "type": "formuesgodetype.mv.e",
                    "typeBeskrivelse": "motorvogn registrert",
                    "identifiseringsmaateFormuesgode": {
                        "registreringsnummerMotorvogn": "CU10103"
                    },
                    "eierandel": {
                        "teller": 1,
                        "nevner": 1
                    }
                }
            ],
            "krav": {
                "belop": [
                    {
                        "belop": 92111.0,
                        "valuta": "NOK"
                    }
                ]
            },
            "paategninger": []
        },
        {
            "dokumentnummer": "2020000127",
            "type": "rettsstiftelsestype.utp",
            "typeBeskrivelse": "Utleggspant",
            "innkomsttidspunkt": "2016-09-22T15:49:58.023",
            "ajourtidspunkt": "2020-05-18T11:05:59.209",
            "status": "statusregistreringsobjekt.tl",
            "statusBeskrivelse": "tinglyst",
            "beslutningstidspunkt": "2020-02-10T09:02:00",
            "roller": [
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.namsmyndighet",
                    "rolletypeBeskrivelse": "Namsmyndighet",
                    "navn": "ENGSTELIG TIGER AS",
                    "forretningsadresse": {
                        "adresse": [ "Stjørdal 123" ],
                        "poststed": "Stjørdal",
                        "postnummer": "7504",
                        "kommune": "Stjørdal",
                        "kommunenummer": "2345",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810843012
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "ENORM TIGER AS",
                    "forretningsadresse": {
                        "adresse": [ "Ålesundgata 123" ],
                        "poststed": "Ålesund",
                        "postnummer": "6011",
                        "kommune": "Ålesund",
                        "kommunenummer": "1234",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810843942
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "LYDIG IDYLL"
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "BLÅ KATT DUEHISTOLOG",
                    "forretningsadresse": {
                        "adresse": [ "Drammensgata 123" ],
                        "poststed": "Drammen",
                        "postnummer": "3044",
                        "kommune": "Drammen",
                        "kommunenummer": "3456",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810864192
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksoker",
                    "rolletypeBeskrivelse": "Saksøker",
                    "navn": "OPPLAGT KUNNSKAP",
                    "adresse": "Kulsrudgutua 2C"
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksoker",
                    "rolletypeBeskrivelse": "Saksøker",
                    "navn": "INNSIKTSFULL BIE"
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksokt",
                    "rolletypeBeskrivelse": "Saksøkt",
                    "navn": "Annie Andersson"
                }
            ],
            "formuesgoder": [
                {
                    "type": "formuesgodetype.mv.e",
                    "typeBeskrivelse": "motorvogn registrert",
                    "identifiseringsmaateFormuesgode": {
                        "registreringsnummerMotorvogn": "CU10102"
                    },
                    "eierandel": {
                        "teller": 1,
                        "nevner": 1
                    }
                },
                {
                    "type": "formuesgodetype.mv.e",
                    "typeBeskrivelse": "motorvogn registrert",
                    "identifiseringsmaateFormuesgode": {
                        "registreringsnummerMotorvogn": "CU10103"
                    },
                    "eierandel": {
                        "teller": 1,
                        "nevner": 1
                    }
                }
            ],
            "krav": {
                "belop": [
                    {
                        "belop": 25000.0,
                        "valuta": "NOK"
                    }
                ]
            },
            "paategninger": []
        },
        {
            "dokumentnummer": "2020000248",
            "type": "rettsstiftelsestype.utp",
            "typeBeskrivelse": "Utleggspant",
            "innkomsttidspunkt": "2016-09-22T15:49:58.023",
            "ajourtidspunkt": "2020-09-23T07:29:08.801",
            "status": "statusregistreringsobjekt.nt",
            "statusBeskrivelse": "nektet tinglyst",
            "beslutningstidspunkt": "2020-09-10T08:02:00",
            "roller": [
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksoker",
                    "rolletypeBeskrivelse": "Saksøker",
                    "navn": "INNSIKTSFULL BIE"
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksokt",
                    "rolletypeBeskrivelse": "Saksøkt",
                    "navn": "Annie Andersson"
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.namsmyndighet",
                    "rolletypeBeskrivelse": "Namsmyndighet",
                    "navn": "ENGSTELIG TIGER AS",
                    "forretningsadresse": {
                        "adresse": [ "Stjørdal 123" ],
                        "poststed": "Stjørdal",
                        "postnummer": "7504",
                        "kommune": "Stjørdal",
                        "kommunenummer": "2345",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810843012
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "ENORM TIGER AS",
                    "forretningsadresse": {
                        "adresse": [ "Ålesundgata 123" ],
                        "poststed": "Ålesund",
                        "postnummer": "6011",
                        "kommune": "Ålesund",
                        "kommunenummer": "1234",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810843942
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "LYDIG IDYLL"
                },
                {
                    "rolleinnehaverType": "VIRKSOMHET",
                    "rolletype": "rolletype.prosessfullmektig",
                    "rolletypeBeskrivelse": "Prosessfullmektig",
                    "navn": "BLÅ KATT DUEHISTOLOG",
                    "forretningsadresse": {
                        "adresse": [ "Drammensgata 123" ],
                        "poststed": "Drammen",
                        "postnummer": "3044",
                        "kommune": "Drammen",
                        "kommunenummer": "3456",
                        "land": "Norge",
                        "landkode": "NO"
                    },
                    "orgnr": 810864192
                },
                {
                    "rolleinnehaverType": "BRPERSON",
                    "rolletype": "rolletype.saksoker",
                    "rolletypeBeskrivelse": "Saksøker",
                    "navn": "OPPLAGT KUNNSKAP",
                    "adresse": "Kulsrudgutua 2C"
                }
            ],
            "formuesgoder": [
                {
                    "type": "formuesgodetype.mv.e",
                    "typeBeskrivelse": "motorvogn registrert",
                    "identifiseringsmaateFormuesgode": {
                        "registreringsnummerMotorvogn": "CU10102"
                    },
                    "eierandel": {
                        "teller": 1,
                        "nevner": 1
                    }
                },
				{
                    "type": "formuesgodetype.mv.e",
                    "typeBeskrivelse": "motorvogn registrert",
                    "identifiseringsmaateFormuesgode": {
                        "registreringsnummerMotorvogn": "CU10103"
                    },
                    "eierandel": {
                        "teller": 1,
                        "nevner": 1
                    }
                }
            ],
            "krav": {
                "belop": [
                    {
                        "belop": 50000.0,
                        "valuta": "NOK"
                    }
                ]
            },
            "paategninger": []
        }
    ]
}
```

---

## Feilmeldinger

Dersom man ikke får HTTP-status 200, så får man en melding fra tjenesten i JSON-format.

| HTTP-kode   | Feilmelding                                                                                 |
|:----------- |:------------------------------------------------------------------------------------------- |
| 400         | Ugyldig orgnr eller sluttbrukerOrgNr                                                                               |
| 403         | Forespørsel inneholder ingen gyldig bearer token                                            |
| 404         | orgnr mangler                                                                               |

##### Eksempelrespons feilmelding

```json
{
    "korrelasjonsid": "c1c188f5-2fe2-4a1b-97f1-360fff37ea21",
    "tidspunkt": "2020-10-28 13:25:53",
    "feilmelding": "Feil i fødselsnummer/organisasjonsnummer, vennligst prøv på nytt"
}
```

---
