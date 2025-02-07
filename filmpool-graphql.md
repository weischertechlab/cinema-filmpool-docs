      
# 1. API für Metadaten

Die API zur Abfrage von Metadaten aus dem Filmpool basiert auf GraphQL.
GraphQL Types mit Queries und Mutations werden mit der Schema Definition Language (SDL) beschrieben
Queries sind lesende Operationen, Mutations sind schreibende Operationen. Mutations sind ausgeschaltet.

[Introduction | Entity GraphQL](https://entitygraphql.github.io/docs/intro)

## 1.1. Machine 2 Machine Authentifizierung & Autorisierung

**OpenID Connect** ([OpenID Connect Protocol](https://auth0.com/docs/authenticate/protocols/openid-connect-protocol))
authority: https://weischer-cinema-dev.eu.auth0.com

**HTTP Authorization Header**
Authorization: Bearer [ACCESS_TOKEN]

## 1.2. Endpunkte

**Methode**: POST
**Pfad**: mediahub-dev.weischer.net/graphql/filmpool
**Abfragesprache**: GraphQL: '{"query": "{

- movies (filter: " ... ")
- foyers (filter: " ... ")
- onlineBanners (filter: " ... ")
- posters (filter: " ... ")
- scenerys (filter: " ... ")
- socialMedias (filter: " ... ")
- titleLettering (filter: " ... ")
- onlineTrailers (filter: " ... ")
- videoclip (filter: " ... ")
- videoContentFoyers (filter: " ... ")
- videoContentLosPosters (filter: " ... ")

}"}'
**Antwortformat**: JSON

[Filtering | Entity GraphQL](https://entitygraphql.github.io/docs/field-extensions/filtering/)

## 1.3. Beispielabfragen

### Metadaten Film

Alle Metadaten für den Film mit der Comscore ID "234935".

Query:
```gql
    {
      movies (filter: "comscoreId = '234935'") {
        id
        originalTitle
        productionCountryCode
        productionYear
        comscoreId
        directors {
          name
          rank
        }
        producers {
          name
          rank
        }
        actors {
          name
          rank
        }
        screenplay {
          name
          rank
        }
        directorsOfPhotography {
          name
          rank
        }
        music {
          name
          rank
        }
        editors {
          name
          rank
        }
        castings {
          name
          rank
        }
        costume {
          name
          rank
        }
        suisaNr
        updatedAt
        movieCountryInfos {
          id
          movieId
          countryCode
          title
          distributor
          startDate
          ageRating
          runningTimeMinutes
          description
          shortDescription
          startDateIsApproved
          ageRatingIsApproved
          updatedAt
        }
      }
    }

```

JSON Result:
```
    {
      "data": {
        "movie": {
          "id": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
          "originalTitle": "How to Train Your Dragon",
          "productionCountryCode": "",
          "productionYear": null,
          "comscoreId": 234935,
          "directors": [
            {
              "name": "Dean DeBlois",
              "rank": null
            }
          ],
          "producers": [],
          "actors": [
            {
              "name": "Gerard Butler",
              "rank": null
            },
            {
              "name": "Mason Thames",
              "rank": null
            },
            {
              "name": "Nick Frost",
              "rank": null
            }
          ],
          "screenplay": [],
          "directorsOfPhotography": [],
          "music": [],
          "editors": [],
          "castings": [
            {
              "name": "Gerard Butler",
              "rank": null
            },
            {
              "name": "Mason Thames",
              "rank": null
            },
            {
              "name": "Nick Frost",
              "rank": null
            },
            {
              "name": "Nico Parker",
              "rank": null
            }
          ],
          "costume": [],
          "suisaNr": null,
          "updatedAt": "2024-11-14T16:38:42.0066667+00:00",
        }
      }
    }

```

### Metadaten Film- und Bildmaterial

Alle Metadaten für den Film mit der Comscore ID "234935" und dessen verfügbaren und gültigen Bildmaterialen von der Kategorie "Foyer" im deutschen Markt.

Query:
```gql
    {
      foyers(filter: "movie.comscoreId = '234935' and countryCode == 'DE' and isContentAvailable == true and isValid == true") {
        movie {
          id
          originalTitle
          productionCountryCode
          productionYear
          comscoreId
          directors {
            name
            rank
          }
          producers {
            name
            rank
          }
          actors {
            name
            rank
          }
          screenplay {
            name
            rank
          }
          directorsOfPhotography {
            name
            rank
          }
          music {
            name
            rank
          }
          editors {
            name
            rank
          }
          castings {
            name
            rank
          }
          costume {
            name
            rank
          }
          suisaNr
          updatedAt
          movieCountryInfos {
            id
            movieId
            countryCode
            title
            distributor
            startDate
            ageRating
            runningTimeMinutes
            description
            shortDescription
            startDateIsApproved
            ageRatingIsApproved
            updatedAt
          }
        }
        id
        movieId
        countryCode
        title
        codec
        colorDepth
        colorSpace
        resolutionWidth
        resolutionHeight
        contentLink
        contentSize
        isContentAvailable
        isValid
        validFrom
        validTo
        updatedAt
      }
    }
```

JSON Result:
```
    {
      "data": {
        "foyers": {
          "movie": {
            "id": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
            "originalTitle": "How to Train Your Dragon",
            "productionCountryCode": "",
            "productionYear": null,
            "comscoreId": 234935,
            "directors": [
              {
                "name": "Dean DeBlois",
                "rank": null
              }
            ],
            "producers": [],
            "actors": [
              {
                "name": "Gerard Butler",
                "rank": null
              },
              {
                "name": "Mason Thames",
                "rank": null
              },
              {
                "name": "Nick Frost",
                "rank": null
              }
            ],
            "screenplay": [],
            "directorsOfPhotography": [],
            "music": [],
            "editors": [],
            "castings": [
              {
                "name": "Gerard Butler",
                "rank": null
              },
              {
                "name": "Mason Thames",
                "rank": null
              },
              {
                "name": "Nick Frost",
                "rank": null
              },
              {
                "name": "Nico Parker",
                "rank": null
              }
            ],
            "costume": [],
            "suisaNr": null,
            "updatedAt": "2024-11-14T16:38:42.0066667+00:00",
            "movieCountryInfos": [
              {
                "id": "6dd7f164-1143-4f74-ae7d-5d096aae057a",
                "movieId": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
                "countryCode": "DE-DE",
                "title": "Drachenzähmen leicht gemacht",
                "distributor": "Universal Pictures International Germany",
                "startDate": "2025-06-12T00:00:00+02:00",
                "ageRating": null,
                "runningTimeMinutes": null,
                "description": "Realfilm-Adaption der beliebten \"Drachenzähmen leicht gemacht\"-Trilogie, bei der abermals Dean DeBlois Regie führen wird. Das Live-Action-Remake erzählt die Geschichte des jungen Wikingers Hicks, der wie seine Freunde und Verwandten Drachenjäger werden will, bevor er auf den verletzten Nachtschatten-Drachen Ohnezahn trifft.",
                "shortDescription": "",
                "startDateIsApproved": null,
                "ageRatingIsApproved": null,
                "updatedAt": "2024-11-14T16:49:22.79+00:00",
              },
              {
                "id": "75c3d116-4d3c-46ca-aa50-2a14f41e3603",
                "movieId": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
                "countryCode": "DE",
                "title": "How to Train Your Dragon",
                "distributor": "Universal Int'l",
                "startDate": "2025-06-12T00:00:00+00:00",
                "ageRating": null,
                "runningTimeMinutes": null,
                "description": "For more than a decade, DreamWorks Animation's epic animated film trilogy about the friendship between a young man and his dragon has moved, inspired and delighted audiences worldwide. Now, a new live-action adaptation of the blockbuster HOW TO TRAIN YOUR DRAGON franchise will transport audiences for the first time into a new cinematic experience and a bold, thrilling new chapter in the beloved story of Viking Hiccup and his Night Fury dragon, Toothless. The film will be written and directed by three-time Academy Award® nominee Dean DeBlois, who has written and directed all three films in animated trilogy (How to Train Your Dragon, How to Train Your Dragon 2, How to Train Your Dragon: The Hidden World). The franchise is based on the best-selling books series by Cressida Cowell. The live-action film will be produced by three-time Oscar® nominee Marc Platt (La La Land, Bridge of Spies), Dean DeBlois and Emmy winner Adam Siegel (2 Guns, Drive). Since 2010, the How to Train Your Dragon films have earned more than $1.6 billion worldwide, have received four Academy Award® nominations and won the Golden Globe award for How to Train Your Dragon 2.",
                "shortDescription": null,
                "startDateIsApproved": false,
                "ageRatingIsApproved": false,
                "updatedAt": "2024-11-19T14:30:59.6333333+00:00",
              }
            ]
          },
          "id": "166bfe5b-cfd7-43fe-ace1-a01e8f6cbc81",
          "movieId": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
          "countryCode": "DE",
          "title": "Banner Teaser 16x9",
          "codec": 1,
          "colorDepth": 8,
          "colorSpace": 1,
          "resolutionWidth": 3840,
          "resolutionHeight": 2160,
          "contentLink": "UPI-Drachenzaehmen-Teaser-16x9.jpg",
          "contentSize": 6299648,
          "isContentAvailable": true,
          "isValid": true,
          "validFrom": "2025-01-28",
          "validTo": "2028-01-28",
          "updatedAt": "2025-01-28T09:10:20.8633333+00:00",
        }
      }
    }
```

### Metadaten Film- und Videomaterial

Alle Metadaten für den Film mit der Comscore ID "123456" und dessen verfügbaren und gültigen Videomaterialien von der Kategorie "Videoclip" im deutschen Markt

Query:
```gql
{
      videoclips (filter: "movie.comscoreId = '234935' and countryCode == 'DE' and isContentAvailable == true and isValid == true") {
        movie {
          id
          originalTitle
          productionCountryCode
          productionYear
          comscoreId
          directors {
            name
            rank
          }
          producers {
            name
            rank
          }
          actors {
            name
            rank
          }
          screenplay {
            name
            rank
          }
          directorsOfPhotography {
            name
            rank
          }
          music {
            name
            rank
          }
          editors {
            name
            rank
          }
          castings {
            name
            rank
          }
          costume {
            name
            rank
          }
          suisaNr
          updatedAt
          movieCountryInfos {
            id
            movieId
            countryCode
            title
            distributor
            startDate
            ageRating
            runningTimeMinutes
            description
            shortDescription
            startDateIsApproved
            ageRatingIsApproved
            updatedAt
          }
        }
        id
        movieId
        countryCode
        title
        codec
        colorDepth
        resolutionWidth
        resolutionHeight
        audioLanguage
        isMute
        dimension
        duration
        frameRate
        colorSpace
        contentLink
        contentSize
        isContentAvailable
        isValid
        validFrom
        validTo
        updatedAt
      }
    }
```

JSON Result:
```
{
  "data": {
    "videoclips": [
      {
        "movie": {
          "id": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
          "originalTitle": "How to Train Your Dragon",
          "productionCountryCode": "",
          "productionYear": null,
          "comscoreId": 234935,
          "directors": [
            {
              "name": "Dean DeBlois",
              "rank": null
            }
          ],
          "producers": [],
          "actors": [
            {
              "name": "Gerard Butler",
              "rank": null
            },
            {
              "name": "Mason Thames",
              "rank": null
            },
            {
              "name": "Nick Frost",
              "rank": null
            }
          ],
          "screenplay": [],
          "directorsOfPhotography": [],
          "music": [],
          "editors": [],
          "castings": [
            {
              "name": "Gerard Butler",
              "rank": null
            },
            {
              "name": " Mason Thames",
              "rank": null
            },
            {
              "name": " Nick Frost",
              "rank": null
            },
            {
              "name": " Nico Parker",
              "rank": null
            }
          ],
          "costume": [],
          "suisaNr": null,
          "updatedAt": "2024-11-14T16:38:42.0066667+00:00",
          "movieCountryInfos": [
            {
              "id": "6dd7f164-1143-4f74-ae7d-5d096aae057a",
              "movieId": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
              "countryCode": "DE-DE",
              "title": "Drachenzähmen leicht gemacht",
              "distributor": "Universal Pictures International Germany",
              "startDate": "2025-06-12T00:00:00+02:00",
              "ageRating": null,
              "runningTimeMinutes": null,
              "description": "Realfilm-Adaption der beliebten \"Drachenzähmen leicht gemacht\"-Trilogie, bei der abermals Dean DeBlois Regie führen wird. Das Live-Action-Remake erzählt die Geschichte des jungen Wikingers Hicks, der wie seine Freunde und Verwandten Drachenjäger werden will, bevor er auf den verletzten Nachtschatten-Drachen Ohnezahn trifft.",
              "shortDescription": "",
              "startDateIsApproved": null,
              "ageRatingIsApproved": null,
              "updatedAt": "2024-11-14T16:49:22.79+00:00",
            },
            {
              "id": "75c3d116-4d3c-46ca-aa50-2a14f41e3603",
              "movieId": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
              "countryCode": "DE",
              "title": "How to Train Your Dragon",
              "distributor": "Universal Int'l",
              "startDate": "2025-06-12T00:00:00+00:00",
              "ageRating": null,
              "runningTimeMinutes": null,
              "description": "For more than a decade, DreamWorks Animation's epic animated film trilogy about the friendship between a young man and his dragon has moved, inspired and delighted audiences worldwide.   Now, a new live-action adaptation of the blockbuster HOW TO TRAIN YOUR DRAGON franchise will transport audiences for the first time into a new cinematic experience and a bold, thrilling new chapter in the beloved story of Viking Hiccup and his Night Fury dragon, Toothless.   The film will be written and directed by three-time Academy Award® nominee Dean DeBlois, who has written and directed all three films in animated trilogy (How to Train Your Dragon, How to Train Your Dragon 2, How to Train Your Dragon: The Hidden World). The franchise is based on the best-selling books series by Cressida Cowell.   The live-action film will be produced by three-time Oscar® nominee Marc Platt (La La Land, Bridge of Spies), Dean DeBlois and Emmy winner Adam Siegel (2 Guns, Drive).   Since 2010, the How to Train Your Dragon films have earned more than $1.6 billion worldwide, have received four Academy Award® nominations and won the Golden Globe award for How to Train Your Dragon 2.",
              "shortDescription": null,
              "startDateIsApproved": false,
              "ageRatingIsApproved": false,
              "updatedAt": "2024-11-19T14:30:59.6333333+00:00",
            }
          ]
        },
        "id": "24174ff0-b7a9-48f0-962f-99b62bc68dcc",
        "movieId": "8e2f3e1e-1e33-4c37-88e2-8859d36bfc96",
        "countryCode": "DE",
        "title": "Featurette First Look",
        "codec": 1,
        "colorDepth": 8,
        "resolutionWidth": 1920,
        "resolutionHeight": 1080,
        "audioLanguage": "DE",
        "isMute": false,
        "dimension": 1,
        "duration": 140,
        "frameRate": 25,
        "colorSpace": 9,
        "contentLink": "Drachenzaehmen_leicht_gemacht_Featurette_First_Look_DE_16x9_OnlineHD.mp4",
        "contentSize": 269135872,
        "isContentAvailable": true,
        "isValid": true,
        "validFrom": "2025-01-29",
        "validTo": "2028-01-29",
        "updatedAt": "2025-01-29T14:37:12.0266667+00:00",
      }
    ]
  }
}
```

## 1.4. Fehlercodes

Verwendung folgender HTTP Statuscodes
**400** Bad request
**401** Unauthorized

# 2. API für Download-Links

Die API zur Abfrage von Metadaten aus dem Filmpool basiert auf REST.

## 2.1. Machine 2 Machine Authentifizierung & Autorisierung

**OpenID Connect** ([OpenID Connect Protocol](https://auth0.com/docs/authenticate/protocols/openid-connect-protocol))
authority: https://weischer-cinema-dev.eu.auth0.com

**HTTP Authorization Header**
Authorization: Bearer [ACCESS_TOKEN]

## 2.2. Endpunkte

**Methode**: GET
**Pfad**: mediahub-dev.weischer.net/api/v1/pictureontents/[id]/download
**Antwortformat**: JSON-Response mit URL

**Methode**: GET
**Pfad**: mediahub-dev.weischer.net/api/v1/videcontents/[id]/download
**Antwortformat**: JSON-Response mit URL

## 2.3. Beispielabfragen

...

## 2.4. Fehlercodes

Verwendung folgender HTTP Statuscodes
**400** Rad request
**401** Unauthoirized
**403** Forbidden
**404** Not found

Verwendung von **Problem Details** für HTTP APIs
[RFC 7807 - Problem Details for HTTP APIs](https://datatracker.ietf.org/doc/html/rfc7807)