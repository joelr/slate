---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://app.justcharity.org/pricing'>Sign Up for an account</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the JustCharity API. You can use our API to access JustCharity API endpoints, which can get information on various events, charities, and analytics within the platform.

Some endpoints are authenticated with an API key, public API endpoints and authenticated endpoints are both documented here.

This API is currently in Beta. Changes may be made at any time, although we aim to avoid breaking changes. If you have any specific integration requirements or use cases and need to confirm implementation details, or have any other enquiries please [Contact us](https://app.justcharity.org/pages/contact).

# API Overview

## Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct get param with each request
curl "https://app.justcharity.org/api/v1/charities/cancer-research-uk/widgets/page.json?api_key=<KEY>"
```

> Make sure to replace `<KEY>` with your API key.

Some endpoints require authentication, although most endpoints are public.

You can register a new JustCharity API key at [JustCharity](https://app.justcharity.org/pricing).

Once you have created an account, you can find the API key under your account page, free accounts are not provided with an API key, but public endpoints can still be accessed.

## Rate limiting

Some endpoints are rate-limited, please ensure any integrations can handle a 429 status code, where possible please implement caching.

## Format

All request/responses are in JSON. However, JSON(P) is also supported for legacy ajax/jquery support.


# Charities

## Get a Specific Charity

```shell
curl "https://app.justcharity.org/api/v1/charities/<SLUG>"
```

> The above command returns JSON structured like this:

```json
{
  "name": "Cancer Research UK",
  "id": 447,
  "slug": "cancer-research-uk",
  "short_title": "Cancer Research UK",
  "engagement_in_period": 565,
  "reach_in_period": 1098478,
  "page_activity_in_period": 259859,
  "page_activity_in_period_percentile": 99.97,
  "reach_in_period_percentile": 99.35,
  "engagement_in_period_percentile": 100
}
```

This endpoint retrieves a specific charity.

### HTTP Request

`GET https://app.justcharity.org/api/v1/charities/<SLUG>`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the charity to retrieve


## Social overview

```shell
curl "https://app.justcharity.org/api/v1/charities/<SLUG>/social"
```

> The above command returns JSON structured like this:

```json
{
  "this_week": {
    "engaged": {
      "count": 151,
      "human_count": "151",
      "data": [
        [
          1466467200000,
          26
        ],
        [
          1466553600000,
          10
        ],
        .......
      ]
    },
    "reach": {
      "count": 282828,
      "human_count": "283K",
      "data": [
        [
          1466467200000,
          41893
        ],
        [
          1466553600000,
          19042
        ],
        .......
      ]
    }
  },
  "last_week": {
    "engaged": {
      "count": 214,
      "human_count": "214",
      "data": [
        [
          1466467200000,
          31
        ],
        [
          1466553600000,
          28
        ],
        .......
      ]
    },
    "reach": {
      "count": 290874,
      "human_count": "291K",
      "data": [
        [
          1466467200000,
          73014
        ],
        [
          1466553600000,
          45419
        ],
        [
          1466640000000,
          42021
        ],
        .......
      ]
    }
  },
  "engaged_change": -30,
  "reach_change": -2.8
}
```

This endpoint retrieves social engagement and reach metrics, for the current and last week.
Engagement details the number of active users on public social media sources engaging with peer to peer fundraising for the specific charity.

This data is used to render the social activity charts:
<img src='/images/social.png' />

### HTTP Request

`GET https://app.justcharity.org/api/v1/charities/<SLUG>/social`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the charity to retrieve



## Hashtags

```shell
curl "https://app.justcharity.org/api/v1/charities/<SLUG>/hash_tags"
```

> The above command returns JSON structured like this:

```json
{
  "hash_tags": [
    {
      "c": 21969,
      "name": "sponsorme"
    },
    {
      "c": 9381,
      "name": "fundraising"
    },
    {
      "c": 8394,
      "name": "justsponsored"
    },
    ....
  ]
}
```

This endpoint retrieves hash tag metrics/mentions for a specific charity.

### HTTP Request

`GET https://app.justcharity.org/api/v1/charities/<SLUG>/hash_tags`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the charity to retrieve


## Engaged pages

```shell
curl "https://app.justcharity.org/api/v1/charities/<SLUG>/pages"
```

> The above command returns JSON structured like this:

```json
{
  "chart_data": [
    ....
  ],
  "data": [
    {
      "count": 69,
      "page": {
        "title": "Panini Cheapskates: Donate Now!",
        "owner_name": "Alex Pratchett, sian pratchett",
        "id": 6806897,
        "provider_url": "https://....",
        "first_donation_at": "2016-06-26T00:00:00.000Z",
        "last_donation_at": "2016-06-26T00:00:00.000Z",
        "charity_id": 447,
        "event_id": null,
        "total_raised": {
          "fractional": "128350.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          }
        },
        "raised_human": "\u00a31,283.50",
        "short_title": "Panini Cheapskates: Donate Now!"
      },
      "page_trend_data": [
        4,
        18,
        2,
        4,
        7,
        2,
        4,
        5,
        4,
        1,
        21,
        5,
        8,
        11,
        1
      ]
    },
    {
      "count": 15,
      "page": {
        "title": "Dawn-to-Dusk 2016's fundraising page",
        "owner_name": "Phil Girling, Adam Keenor, Elliott Hooper-Nash, Simon Burns, Max Ireland, John Hall, Bethan Keeble, Richard Frederick, Alex Sprague, Gareth Jones, Roger Cutts, Matthew Hardy, Jason Lewis, Oliver Fitzgerald-Lombard, Tim Thorpe,",
        "id": 6758017,
        "provider_url": "https://....",
        "first_donation_at": "2016-06-20T00:00:00.000Z",
        "last_donation_at": "2016-06-20T00:00:00.000Z",
        "charity_id": 447,
        "event_id": null,
        "total_raised": {
          "fractional": "180600.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          }
        },
        "raised_human": "\u00a31,806.00",
        "short_title": "Dawn-to-Dusk 2016&#39;s fundraising ..."
      },
      "page_trend_data": [
        7,
        8
      ]
    },
    ......
  ]
}
```

This endpoint retrieves a list of recently socially active pages for the specific charity.

### HTTP Request

`GET https://app.justcharity.org/api/v1/charities/<SLUG>/pages`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the charity to retrieve


## Engaged events

```shell
curl "https://app.justcharity.org/api/v1/charities/<SLUG>/events"
```

> The above command returns JSON structured like this:

```json
{
  "chart_data": [
    ...
  ],
  "data": [
    {
      "count": 13,
      "event": {
        "name": "Guildford 5K 2016 11:00",
        "id": 1226300,
        "slug": "guildford-5k-2016-11-00",
        "start_at": "2016-06-26T00:00:00.000Z",
        "short_title": "Guildford 5K 2016 11:00",
        "total_raised": {
          "fractional": "2816936.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          },
          "bank": {
            "rounding_method": null,
            "rates": {
              
            },
            "mutex": {
              
            }
          }
        },
        "total_raised_offline": {
          "fractional": "34000.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          },
          "bank": {
            "rounding_method": null,
            "rates": {
              
            },
            "mutex": {
              
            }
          }
        },
        "total_raised_online": {
          "fractional": "2763036.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          },
          "bank": {
            "rounding_method": null,
            "rates": {
              
            },
            "mutex": {
              
            }
          }
        },
        "engagement_in_period": 14,
        "reach_in_period": 22413,
        "page_activity_in_period": 207,
        "page_activity_in_period_percentile": 99.66,
        "reach_in_period_percentile": 89.78,
        "engagement_in_period_percentile": 93.15
      },
      "event_trend_data": [
        3,
        8,
        1,
        1
      ]
    },
    {
      "count": 11,
      "event": {
        "name": "Bradford 5K 2016 10:30",
        "id": 1066907,
        "slug": "bradford-5k-2016-10-30",
        "start_at": "2016-06-11T00:00:00.000Z",
        "short_title": "Bradford 5K 2016 10:30",
        "total_raised": {
          "fractional": "3264527.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          },
          "bank": {
            "rounding_method": null,
            "rates": {
              
            },
            "mutex": {
              
            }
          }
        },
        "total_raised_offline": {
          "fractional": "164400.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          },
          "bank": {
            "rounding_method": null,
            "rates": {
              
            },
            "mutex": {
              
            }
          }
        },
        "total_raised_online": {
          "fractional": "3073327.0",
          "currency": {
            "id": "gbp",
            "priority": 3,
            "iso_code": "GBP",
            "name": "British Pound",
            "symbol": "\u00a3",
            "alternate_symbols": [
              
            ],
            "subunit": "Penny",
            "subunit_to_unit": 100,
            "symbol_first": true,
            "html_entity": "&#x00A3;",
            "decimal_mark": ".",
            "thousands_separator": ",",
            "iso_numeric": "826"
          },
          "bank": {
            "rounding_method": null,
            "rates": {
              
            },
            "mutex": {
              
            }
          }
        },
        "engagement_in_period": 12,
        "reach_in_period": 29058,
        "page_activity_in_period": 433,
        "page_activity_in_period_percentile": 99.9,
        "reach_in_period_percentile": 91.23,
        "engagement_in_period_percentile": 91.55
      },
      "event_trend_data": [
        1,
        10
      ]
    },
    ....
  ]
}
```

This endpoint retrieves a list of recently socially active events for the specific charity.

### HTTP Request

`GET https://app.justcharity.org/api/v1/charities/<SLUG>/events`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the charity to retrieve




## Page Widget

```shell
curl "https://app.justcharity.org/api/v1/charities/<SLUG>/widgets/page.json?api_key=<KEY>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "title": "Walk for Life as quick as I can!",
    "owner_name": "Donna Jones",
    "clean_url": "http://www.raceforlifesponsorme.org/DonnaWynneJones",
    "first_donation_at": null,
    "last_donation_at": null,
    "charity": "Cancer Research UK",
    "event": "Cardiff",
    "total_raised_cents": 2000,
    "raised_human": "£20.00",
    "donation_count": 2,
    "image_url": null
  },
  {
    "title": "Louise Bromley's Fundraising Page",
    "owner_name": "Louise Bromley",
    "clean_url": "http://www.raceforlifesponsorme.org/LOUISEBROMLEY",
    "first_donation_at": null,
    "last_donation_at": null,
    "charity": "Cancer Research UK",
    "event": "Basingstoke",
    "total_raised_cents": 1500,
    "raised_human": "£15.00",
    "donation_count": 3,
    "image_url": null
  },
  {
    "title": "Sponsor me!!",
    "owner_name": "Olivia Forster",
    "clean_url": "http://www.raceforlifesponsorme.org/OliviaForster",
    "first_donation_at": null,
    "last_donation_at": null,
    "charity": "Cancer Research UK",
    "event": "Leeds (Temple Newsam)",
    "total_raised_cents": 5000,
    "raised_human": "£50.00",
    "donation_count": 6,
    "image_url": null
  },
  .......
]
```

This endpoint retrieves a list of recent pages for a charity.

### HTTP Request

`GET https://app.justcharity.org/api/v1/charities/<SLUG>/widgets/page.json?api_key=<KEY>`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the charity to retrieve

## Social Widget

```shell
curl "https://app.justcharity.org/api/v1/charities/<SLUG>/widgets/social.json?api_key=<KEY>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "user": {
    "photo": "https://pbs.twimg.com/profile_images/490984326830772225/WTEvX65N_400x400.jpeg",
    "url": "https://twitter.com/jemmataylor1989",
    "name": "jemma"
  },
  "page": {
    "title": "Luke's Family's fundraising page",
    "owner_name": "Katrina Francis, Ian Francis, Jemma Taylor, Christopher Taylor, barbara Fuge, Jasmin Eames, Sophie Procter",
    "clean_url": "http://uk.virginmoneygiving.com/fundraiser-web/fundraiser/showFundraiserProfilePage.action?userUrl=IanKatrinaFrancis&isTeam=true",
    "first_donation_at": null,
    "last_donation_at": "2016-06-18T00:00:00.000Z",
    "charity": "Cardiac Risk in the Young",
    "event": "CRY Heart of London Bridges Walk",
    "total_raised_cents": 72500,
    "raised_human": "£725.00",
    "donation_count": 44,
    "image_url": null
    }
  },
  {
  "user": {
    "photo": "https://pbs.twimg.com/profile_images/637592970733166593/gxbF5qv2_400x400.jpg",
    "url": "https://twitter.com/ryanbingbong",
    "name": "Ryan Newman"
  },
  "page": {
    "title": "Letcombe Two's fundraising page",
    "owner_name": "Tom Sutherland",
    "clean_url": "http://uk.virginmoneygiving.com/fundraiser-web/fundraiser/showFundraiserPage.action?userUrl=TomSutherland&pageUrl=3",
    "first_donation_at": "2016-06-01T00:00:00.000Z",
    "last_donation_at": "2016-06-26T00:00:00.000Z",
    "charity": "Cardiac Risk in the Young",
    "event": "CRY Heart of London Bridges Walk",
    "total_raised_cents": 19150,
    "raised_human": "£191.50",
    "donation_count": 14,
    "image_url": null
    }
  },
  {
  "user": {
    "photo": "https://pbs.twimg.com/profile_images/2678102757/524d2b468f696f667b94aa76b3487338_400x400.jpeg",
    "url": "https://twitter.com/tas9173",
    "name": "Tom Sutherland"
  },
  "page": {
    "title": "Letcombe Two's fundraising page",
    "owner_name": "Tom Sutherland",
    "clean_url": "http://uk.virginmoneygiving.com/fundraiser-web/fundraiser/showFundraiserPage.action?userUrl=TomSutherland&pageUrl=3",
    "first_donation_at": "2016-06-01T00:00:00.000Z",
    "last_donation_at": "2016-06-26T00:00:00.000Z",
    "charity": "Cardiac Risk in the Young",
    "event": "CRY Heart of London Bridges Walk",
    "total_raised_cents": 19150,
    "raised_human": "£191.50",
    "donation_count": 14,
    "image_url": null
    }
  },
  .......
]
```

This endpoint retrieves a list of social activity for pages for a charity.

### HTTP Request

`GET https://app.justcharity.org/api/v1/charities/<SLUG>/widgets/social.json?api_key=<KEY>`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the charity to retrieve



# Events

## Get a Specific Event

```shell
curl "https://app.justcharity.org/api/v1/events/dryathlon-2015"
```

> The above command returns JSON structured like this:

```json
{
  "name": "Dryathlon 2015",
  "id": 829692,
  "slug": "dryathlon-2015",
  "start_at": "2015-01-31T00:00:00.000Z",
  "short_title": "Dryathlon 2015",
  "total_raised": {
    "fractional": "388053056.0",
    "currency": {
      "id": "gbp",
      "priority": 3,
      "iso_code": "GBP",
      "name": "British Pound",
      "symbol": "£",
      "alternate_symbols": [],
      "subunit": "Penny",
      "subunit_to_unit": 100,
      "symbol_first": true,
      "html_entity": "&#x00A3;",
      "decimal_mark": ".",
      "thousands_separator": ",",
      "iso_numeric": "826"
    },
    "bank": {
      "rounding_method": null,
      "rates": {},
      "mutex": {}
    }
  },
  "total_raised_offline": {
    "fractional": "18856792.0",
    "currency": {
      "id": "gbp",
      "priority": 3,
      "iso_code": "GBP",
      "name": "British Pound",
      "symbol": "£",
      "alternate_symbols": [],
      "subunit": "Penny",
      "subunit_to_unit": 100,
      "symbol_first": true,
      "html_entity": "&#x00A3;",
      "decimal_mark": ".",
      "thousands_separator": ",",
      "iso_numeric": "826"
    },
    "bank": {
      "rounding_method": null,
      "rates": {},
      "mutex": {}
    }
  },
  "total_raised_online": {
    "fractional": "357612864.0",
    "currency": {
      "id": "gbp",
      "priority": 3,
      "iso_code": "GBP",
      "name": "British Pound",
      "symbol": "£",
      "alternate_symbols": [],
      "subunit": "Penny",
      "subunit_to_unit": 100,
      "symbol_first": true,
      "html_entity": "&#x00A3;",
      "decimal_mark": ".",
      "thousands_separator": ",",
      "iso_numeric": "826"
    },
    "bank": {
      "rounding_method": null,
      "rates": {},
      "mutex": {}
    }
  },
  "engagement_in_period": 0,
  "reach_in_period": 0,
  "page_activity_in_period": 28,
  "page_activity_in_period_percentile": 97.75,
  "reach_in_period_percentile": 0,
  "engagement_in_period_percentile": 0
}
```

This endpoint retrieves a specific event.

### HTTP Request

`GET https://app.justcharity.org/api/v1/events/<SLUG>`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the event to retrieve


## Hashtags

```shell
curl "https://app.justcharity.org/api/v1/events/<SLUG>/hash_tags"
```

> The above command returns JSON structured like this:

```json
{
  "hash_tags": [
    {
      "c": 21969,
      "name": "sponsorme"
    },
    {
      "c": 9381,
      "name": "fundraising"
    },
    {
      "c": 8394,
      "name": "justsponsored"
    },
    ....
  ]
}
```

This endpoint retrieves hash tag metrics/mentions for a specific event.

### HTTP Request

`GET https://app.justcharity.org/api/v1/event/<SLUG>/hash_tags`

### URL Parameters

Parameter | Description
--------- | -----------
SLUG | The SLUG of the event to retrieve

