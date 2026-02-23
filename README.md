![Expedia Scraper Featured Image](https://raw.githubusercontent.com/omkarcloud/expedia-scraper/master/expedia-scraper-featured-image.png)

# Expedia Scraper API

Search airports, compare one-way flights, and get real-time fares with full itineraries, cabin tiers, and booking links — all from a single API call. No scraping infra needed. 5,000 free requests/month.

## Key Features

- Search airports worldwide by city name, airport name, or IATA code
- Find one-way flights with 30+ data points per offer (price, airlines, layovers, amenities)
- Get multiple fare tiers per flight (Basic, Economy, Comfort, Premium) with inclusion details
- Segment-by-segment itineraries with flight numbers, aircraft types, and layover info
- Direct Expedia booking URLs for each fare option
- **5,000 requests/month on free tier**
- Contact us if you need Expedia Hotels, Car Rentals, Packages, or other data in addition to flights. Reach out [here](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20Expedia%20Scraper%20API.)
- Example Response:
```json
{
    "departure_time": "8:20am",
    "arrival_time": "8:32pm",
    "headline": "Los Angeles to New York",
    "duration_summary": "8:20am - 8:32pm (9h 12m, 2 stops)",
    "starting_price": "$948",
    "stop_count": 2,
    "onboard_amenities": ["Wi-Fi", "In-seat power outlet", "In-flight entertainment"],
    "airlines": [{"name": "Multiple airlines"}],
    "fare_options": [
        {
            "fare_name": "Economy",
            "display_price": "$948",
            "inclusions": [
                {"label": "Seat choice included", "fee": null},
                {"label": "Carry-on bag included", "fee": null},
                {"label": "1st checked bag:", "fee": "$40"}
            ]
        }
    ]
}
```

## Get API Key

Create an account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up?redirect=/api-key) to get your API key.

It takes just 2 minutes to sign up. You get 5,000 free requests every month — more than enough for most users to get their job done without paying a dime.

This is a well built product, and your search for the best Expedia Scraper API ends right here.


## Quick Start

```bash
curl -X GET "https://expedia-scraper.omkar.cloud/expedia/flights/one-way?departure_airport_code=LAX&arrival_airport_code=JFK" \
  -H "API-Key: YOUR_API_KEY"
```

```json
{
    "total_results": 14,
    "flights": [
        {
            "departure_time": "8:20am",
            "arrival_time": "8:32pm",
            "headline": "Los Angeles to New York",
            "duration_summary": "8:20am - 8:32pm (9h 12m, 2 stops)",
            "starting_price": "$948",
            "fare_type": "One way per traveler",
            "stop_count": 2,
            "onboard_amenities": ["Wi-Fi", "In-seat power outlet", "In-flight entertainment"],
            "airlines": [{"name": "Multiple airlines"}],
            "fare_options": [
                {
                    "fare_name": "Economy",
                    "display_price": "$948",
                    "inclusions": [
                        {"label": "Seat choice included", "fee": null},
                        {"label": "Carry-on bag included", "fee": null},
                        {"label": "1st checked bag:", "fee": "$40"}
                    ],
                    "booking_url": "https://www.expedia.com/Flight-Information?..."
                }
            ]
        }
    ]
}
```

## Quick Start (Python)

```bash
pip install requests
```

```python
import requests

# Search one-way flights
response = requests.get(
    "https://expedia-scraper.omkar.cloud/expedia/flights/one-way",
    params={
        "departure_airport_code": "LAX",
        "arrival_airport_code": "JFK",
        "cabin_class": "coach",
    },
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```


## API Reference

### Airport Search

```
GET https://expedia-scraper.omkar.cloud/expedia/flights/airports
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `keyword` | Yes | — | Search text to find airports. City name, airport name, or IATA code. |

#### Example

```python
import requests

response = requests.get(
    "https://expedia-scraper.omkar.cloud/expedia/flights/airports",
    params={"keyword": "london"},
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
    "total_results": 7,
    "locations": [
        {
            "region_id": "6139104",
            "location_type": "METROCODE",
            "name": "London (LON - All Airports)",
            "full_name": "London, United Kingdom (LON-All Airports)",
            "short_name": "London (LON-All Airports)",
            "display_label": "London (LON - All Airports), United Kingdom",
            "secondary_label": "United Kingdom",
            "latitude": "51.54783319395783",
            "longitude": "0.021250695442023394",
            "country": {
                "name": "United Kingdom",
                "code": "GB",
                "code_alpha3": "GBR"
            },
            "airport": {
                "iata_code": "LON",
                "airport_id": "6139104",
                "metro_code": "LON",
                "multi_city_id": "178279"
            },
            "distance_from_center": null,
            "is_minor_airport": false
        },
        {
            "region_id": "5392460",
            "location_type": "AIRPORT",
            "name": "London (LHR - Heathrow)",
            "full_name": "London, United Kingdom (LHR-Heathrow)",
            "short_name": "London (LHR-Heathrow)",
            "display_label": "London (LHR - Heathrow), 23 km from city centre",
            "secondary_label": "23 km from city centre",
            "latitude": "51.470878",
            "longitude": "-0.449753",
            "country": {
                "name": "United Kingdom",
                "code": "GB",
                "code_alpha3": "GBR"
            },
            "airport": {
                "iata_code": "LHR",
                "airport_id": "5392460",
                "metro_code": "LON",
                "multi_city_id": "178279"
            },
            "distance_from_center": {
                "km": 22.66774624656282,
                "miles": 14.085119518910124
            },
            "is_minor_airport": false
        }
    ]
}
```

</details>

---

### One-Way Flight Search

```
GET https://expedia-scraper.omkar.cloud/expedia/flights/one-way
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `departure_airport_code` | Yes | — | IATA code of the departure airport (e.g., `LAX`). |
| `arrival_airport_code` | Yes | — | IATA code of the destination airport (e.g., `JFK`). |
| `departure_date` | No | tomorrow | Travel date in `YYYY-MM-DD` format. Must be today or a future date. |
| `cabin_class` | No | `coach` | `coach`, `premium_economy`, `business`, `first` |

#### Example

```python
import requests

response = requests.get(
    "https://expedia-scraper.omkar.cloud/expedia/flights/one-way",
    params={
        "departure_airport_code": "LAX",
        "arrival_airport_code": "JFK",
        "departure_date": "2026-03-15",
        "cabin_class": "coach",
    },
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response Fields

Returns 30+ fields per flight offer including departure/arrival times, duration, stop count, starting price, airline name and logo, full segment-by-segment itinerary, multiple fare tiers with pricing, fare inclusions (seat, bags, refund policy, change fees), booking URLs, and onboard amenities.

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
    "total_results": 14,
    "flights": [
        {
            "offer_id": "eyJkIjp7ImoiOl...",
            "departure_time": "8:20am",
            "arrival_time": "8:32pm",
            "time_range": "8:20am - 8:32pm",
            "headline": "Los Angeles to New York",
            "travel_date": "Mon, Feb 23",
            "duration_summary": "8:20am - 8:32pm (9h 12m, 2 stops)",
            "starting_price": "$948",
            "fare_type": "One way per traveler",
            "stop_count": 2,
            "onboard_amenities": ["Wi-Fi", "In-seat power outlet", "In-flight entertainment"],
            "airlines": [
                {
                    "name": "Multiple airlines",
                    "logo_url": "https://images.trvl-media.com/media/content/expus/graphics/static_content/fusion/v0.1b/images/airlines/s/multiple_airlines_logo_sq.jpg"
                }
            ],
            "itineraries": [
                {
                    "route": "Los An... (LAX) - New York (JFK)",
                    "travel_time": "9h 12m (2 stops)",
                    "arrives_next_day": null,
                    "layover_summary": "47m in IAH • 34m in BNA",
                    "operated_by": "• Delta 4909 operated by Endeavor Air DBA Delta Connection",
                    "urgency": "1 left at",
                    "segments": [
                        {
                            "origin_airport": "Los Angeles Intl. (LAX)",
                            "origin_code": "LAX",
                            "origin_city": "Los Angeles",
                            "departure_time": "8:20am",
                            "destination_airport": "George Bush Intercontinental (IAH)",
                            "destination_code": "IAH",
                            "destination_city": "Houston",
                            "arrival_time": "1:38pm",
                            "details": [
                                "3h 18m flight",
                                "United 1416",
                                "Boeing 737-900",
                                "Economy/Coach (U)"
                            ],
                            "layover_note": "Layover: 47m in Houston"
                        },
                        {
                            "origin_airport": "George Bush Intercontinental (IAH)",
                            "origin_code": "IAH",
                            "origin_city": "Houston",
                            "departure_time": "2:25pm",
                            "destination_airport": "Nashville Intl. (BNA)",
                            "destination_code": "BNA",
                            "destination_city": "Nashville",
                            "arrival_time": "4:26pm",
                            "details": [
                                "2h 1m flight",
                                "United 1540",
                                "Boeing 737 MAX 8",
                                "Economy/Coach (U)"
                            ],
                            "layover_note": "Layover: 34m in Nashville"
                        },
                        {
                            "origin_airport": "Nashville Intl. (BNA)",
                            "origin_code": "BNA",
                            "origin_city": "Nashville",
                            "departure_time": "5:00pm",
                            "destination_airport": "John F. Kennedy Intl. (JFK)",
                            "destination_code": "JFK",
                            "destination_city": "New York",
                            "arrival_time": "8:32pm",
                            "details": [
                                "2h 32m flight",
                                "Delta 4909 operated by Endeavor Air DBA Delta Connection",
                                "Canadair Regional Jet 900",
                                "Economy/Coach (K)"
                            ],
                            "layover_note": null
                        }
                    ]
                }
            ],
            "fare_options": [
                {
                    "fare_name": "Economy",
                    "cabin": "Cabin: Economy",
                    "display_price": "$948",
                    "price_detail": "$947.33 one way for 1 traveler",
                    "original_price": null,
                    "inclusions": [
                        {"label": "Seat choice included", "fee": null},
                        {"label": "Personal item included", "fee": null},
                        {"label": "Carry-on bag included", "fee": null},
                        {"label": "1st checked bag:", "fee": "$40"},
                        {"label": "Non-refundable", "fee": null},
                        {"label": "Changes included, only pay fare difference", "fee": null}
                    ],
                    "booking_url": "https://www.expedia.com/Flight-Information?journeyContinuationId=..."
                }
            ],
            "badges": []
        }
    ]
}
```

</details>

## Error Handling

```python
response = requests.get(
    "https://expedia-scraper.omkar.cloud/expedia/flights/one-way",
    params={"departure_airport_code": "LAX", "arrival_airport_code": "JFK"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## FAQs

### What data does the API return?

**Airport Search** returns region ID, location type (airport, metro area, city), full/short/display names, IATA code, airport ID, metro code, latitude, longitude, country (name + ISO codes), and distance from city center in km and miles.

**One-Way Flight Search** returns 30+ fields per offer — departure/arrival times, duration, stop count, starting price, airline name and logo, full segment-by-segment itinerary (airports, flight numbers, aircraft types, layover info), multiple fare tiers with individual pricing, fare inclusions (seat choice, bags, refund policy, change fees), booking URLs, and onboard amenities.

All in structured JSON. Ready to use in your app.

### How accurate is the data?

Data is pulled from Expedia in real time. Every API call fetches live data — not cached or stale results. Prices, availability, and itineraries reflect what's on Expedia right now.

### What airports and routes are supported?

Any airport or route available on Expedia. That covers thousands of airports worldwide. Use the Airport Search endpoint to find IATA codes for any city, then pass those codes to the flight search. Works for domestic and international routes.

### Can I search different cabin classes?

Yes. Pass `cabin_class` with one of: `coach`, `premium_economy`, `business`, `first`. Defaults to `coach` if not specified.

### Do I get booking links?

Yes. Every fare option includes a direct `booking_url` to Expedia's booking page for that specific flight and fare tier.

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Questions? We have answers.

Reach out anytime. We will solve your query within 1 working day.

[![Contact Us on WhatsApp about Expedia Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20Expedia%20Scraper%20API.)

[![Contact Us on Email about Expedia Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=Expedia%20Scraper%20API%20Question)
