# Google Hotels Scraper

![Google Hotels Scraper](https://raw.githubusercontent.com/smoldesk/apify-scrapers/main/assets/google-hotels/banner.webp)

Scrape Google Hotels prices, ratings and booking sites for any city, neighborhood or landmark. Your dates, guests and currency. No login. Runs on [Apify](https://apify.com/smoldesk/google-hotels-scraper).

## What you get

- **Prices**: nightly price, total stay, and the split into before taxes and taxes and fees.
- **Ratings**: hotel class, score, review count, star distribution and review aspects such as Service or Room amenities.
- **Location**: coordinates, country code, website, check-in and check-out times and nearby places with travel time.
- **Contact and amenities**: address, phone, Google Maps link, amenities list, deal label like "19% less than usual".
- **Booking-site prices** (optional): the sites Google lists for a hotel with each site's price, free-cancellation deadline, direct booking link when Google gives one, a `cheapestListedSite`, and the hotel's Tripadvisor score.
- **Reviews** (optional): full text of Google reviews, rating, reviewer, owner's reply and photos.
- **Google's own filters and sort**: lowest price, highest rating or most reviewed; amenities, star classes, free cancellation, deals only, eco-certified, property types. Plus max price per night and only hotels with a price.
- **Vacation rentals**: apartments and houses with sleeps, bedrooms, bathrooms and beds.
- **Relative dates** like `+30 days` for scheduled rate trackers.
- **Photos**: up to `maxPhotos` per hotel at 1200 px width.

## Run it

Open the [Google Hotels Scraper on Apify](https://apify.com/smoldesk/google-hotels-scraper), fill in the form and click Start. Or call it from code with your [Apify token](https://console.apify.com/settings/integrations):

```bash
curl -X POST "https://api.apify.com/v2/acts/smoldesk~google-hotels-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "locations": ["Barcelona", "Lisbon"],
    "checkInDate": "2026-12-10",
    "checkOutDate": "2026-12-13",
    "adults": 2,
    "currency": "EUR",
    "minRating": "4",
    "sortBy": "lowest_price",
    "amenities": ["pool"],
    "freeCancellation": true,
    "maxResultsPerLocation": 100,
    "includePrices": true,
    "maxReviewsPerHotel": 10
  }'
```

## Sample output

```json
{
  "type": "hotel",
  "searchLocation": "London",
  "position": 1,
  "name": "The Tower Hotel, by Thistle",
  "hotelClass": 4,
  "rating": 4.1,
  "reviewCount": 12649,
  "pricePerNight": 151.82,
  "totalPrice": 364.38,
  "totalBeforeTaxes": 303.64,
  "totalTaxesAndFees": 60.73,
  "currency": "USD",
  "checkIn": "2026-10-29",
  "checkOut": "2026-10-31",
  "nights": 2,
  "latitude": 51.506786,
  "longitude": -0.0739649,
  "cheapestListedSite": "Expedia.com",
  "bookingSitePrices": [{"site": "Expedia.com", "pricePerNight": 133, "totalPrice": 287}]
}
```

Export as JSON, CSV or Excel, or pipe it into Google Sheets, Make, Zapier or n8n.

## Pricing

Pay per result. No monthly fee. Prices drop on paid Apify plans.

| Result (per 1,000) | Free | Starter | Scale | Business |
|---|---|---|---|---|
| Hotel | $2.50 | $2.50 | $2.20 | $1.90 |
| Booking-site prices for a hotel (optional add-on) | +$2.00 | +$2.00 | +$1.75 | +$1.50 |
| Review (optional) | $0.60 | $0.60 | $0.50 | $0.40 |

Hotels Google does not return are not charged.

## Limits

- Prices are what Google Hotels shows for your dates. Some hotels show no price. Use `onlyWithPrice` to drop them.
- Google picks which booking sites to list, usually 3 to 6. The lowest search price may come from a site missing from that list.
- Google lists up to a few thousand hotels per location. Search by neighborhood for deeper coverage of big cities.
- Reviews show how long ago they were written, not the exact date. Reviews from other sites keep their full text on those sites.
- Some search results carry no address; the full address is filled from the hotel page when `includePrices` is on.

## FAQ

**Is there an official Google Hotels API?**
Not a public one. This reads the Google Travel pages any visitor sees.

**Can I get prices in my currency?**
Yes. Set `currency` to `EUR`, `GBP`, `MYR` or any code Google supports.

**How do I track hotel prices every day?**
Schedule the run with the same `locations` or `hotelUrls` and future dates, then compare `pricePerNight` between runs.

**Can I scrape one specific hotel?**
Yes. Paste its Google Hotels link into `hotelUrls`.

**Can I get a price for every date for one hotel?**
Yes, with the [Google Hotels Price Calendar](https://github.com/smoldesk/google-hotel-price-calendar): the cheapest rate for each check-in date up to a year ahead.

**Do I need an account or a proxy?**
No. Requests go out from the run's own IP. If Google starts answering with captcha pages, the Actor slows down and stops early with what it has.

## More scrapers

Google Hotels is one of 21 no-login scrapers by Smoldesk Studios. See the full list: [smoldesk/apify-scrapers](https://github.com/smoldesk/apify-scrapers).
