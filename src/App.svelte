<script>
	import BigNumber from 'bignumber.js';
	import countries from './inputs/Country.json';
	import currencyCode from './inputs/CurrencyCode.json';
	import portfolio from './inputs/portfolio.json';

	const portfolios = portfolio.portfolios
	.map(portfolio => {
		portfolio.fxAssets = portfolio.fxAssets.map(asset => {
			asset.amount = new BigNumber(asset.amount);
			return asset;
		})
		return portfolio;
	});
	export const promise = new Promise((resolve, reject) =>
		fetch('https://openexchangerates.org/api/latest.json?app_id=925b5c034e404a678862b0ea49a2fab6')
		.then(function(response) {
			let result = response.json();
			return result;
		})
		.then(res => {
			let rates = res.rates;
			let portfoliosDisplay = portfolios
			.map((p, i) => {
				const nativeCountry = countries.find(country => country.code === p.countryCode);
				const nativeCurrency = currencyCode
					.find(currency => currency.isoCode === nativeCountry.currencyCode);
				const totalValueUSD = p.fxAssets
					.reduce((total, asset) => {
						let conversionRate = rates[asset.currencyCode];
						return asset.amount.times(conversionRate).plus(total);
					}, 0);
				return {
					name: p.name,
					countryCode: nativeCountry.name,
					currencySymbol: nativeCurrency.symbol,
					bigNumberValue: totalValueUSD,
					totalValueUSD: totalValueUSD.toFormat(2),
					totalValueNative: totalValueUSD.times(rates[nativeCurrency.isoCode]).toFormat(2)
				};
			})
			.sort((a, b) => {
				const diff = b.bigNumberValue.minus(a.bigNumberValue).toNumber()
				return diff;
			});
			resolve(portfoliosDisplay);
		})
	);
	export let name;
</script>

<style>
	td,
	th {
		padding: 5px 12px
	}
</style>

{#await promise then portfolios}
<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Portfolio Value</th>
			<th>Portfolio Value (USD)</th>
		</tr>
	</thead>
	<tbody>
		{#each portfolios as portfolio}
			<tr>
				<td>{portfolio.name}</td>
				<td>{portfolio.currencySymbol}{portfolio.totalValueNative}</td>
				<td>${portfolio.totalValueUSD}</td>
			</tr>
		{/each}
	</tbody>
</table>
{/await}