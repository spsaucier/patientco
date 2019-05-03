## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.


## Deploying to the web

### With [now](https://zeit.co/now)

Install `now` if you haven't already:

```bash
npm install -g now
```

Then, from within your project folder:

```bash
now
```

As an alternative, use the [Now desktop client](https://zeit.co/download) and simply drag the unzipped project folder to the taskbar icon.

Currently running at https://patientco-test.spsaucier.now.sh/public/


### Original Instructions:
Your job is to create a small foreign exchange portfolio app. You'll have 4 JSON data sources to ingest:

- portfolio.json - a list of portfolios. Each contains a name, a nationality and a list currencies in various denominations
- CurrencyCode.json - a list of currencies and what country they are associated with
- Country.json - a list of Nationalities and the CurrencyCode associated with that country
- A live exchange rate feed: http://openexchangerates.org/api/latest.json?app_id=925b5c034e404a678862b0ea49a2fab6

Write JS+HTML app that takes the input from the above sources and lists each person's name, nationality and the total value of their portfolio in the currency of their home country. The list of portfolios should be sorted by their intrinsic value. Objective is to see your process and coding/learning skills. Documentation of code might be important.
If possible use github to post your code and host it.