<script>
	import ExternalLink from '@svizzle/ui/src/ExternalLink.svelte';
	import LinkButton from '@svizzle/ui/src/LinkButton.svelte';

	import {screenGauge} from 'app/components/ScreenGauge.svelte';

	const crunchbaseUrl = 'https://www.crunchbase.com/';
	const DelgadoEtAlUrl = 'https://www.nber.org/papers/w20375.pdf';
	const eurostatUrl = 'https://ec.europa.eu/eurostat';
	const HausmanAndHidalgoUrl = 'https://www.pnas.org/content/106/26/10570';
	const hesaUrl = 'https://www.hesa.ac.uk';
	const lepUrl = 'https://geoportal.statistics.gov.uk/search?collection=Dataset&sort=name&tags=all(BDY_LEP)';
	const MateosGarciaUrl = 'https://osf.io/preprints/socarxiv/3cu67';
	const nutsUrl = 'https://ec.europa.eu/eurostat/web/gisco/geodata/reference-data/administrative-units-statistical-units/nuts';
	const onsUrl = 'https://ons.gov.uk';
	const patstatUrl = 'https://www.epo.org/searching-for-patents/business/patstat.html';
	const ukriUrl = 'https://www.ukri.org/';
</script>

<svelte:head>
	<title>EURITO CSVs - Methodology</title>
</svelte:head>

<main class={$screenGauge?.classes}>
	<section>
		<h1>Methodology</h1>

		<h2>Data sources</h2>

		<p>As much as possible we have used data from official sources such as <a href={onsUrl}>ONS</a>, <a href={eurostatUrl}>Eurostat</a>, <a href={hesaUrl}>HESA</a> or <a href={ukriUrl}>UKRI</a>. One reason to do this is to enable the reproducibility of our analysis, and to remove the reliance of the tool on proprietary sources.<p>
		<p>Having said this, in a small number of instances we have used proprietary data sources such as <a href={patstatUrl}>PATSTAT</a> for the analysis of patenting, and <a href={crunchbaseUrl}>Crunchbase</a> for the analysis of venture capital investment.<p>

		<h2>Geographies</h2>

		<p>We use <a href={nutsUrl}>NUTS2</a> regions as our geographical unit of analysis. This has allowed us to collect data about regional R&D activity which is only available at that level. We note that were possible we have also calculated indicators at a higher level of granularity (NUTS3) as well as using policy-relevant <a href={lepUrl}>LEP</a>s boundaries. These will be released when the tool is published later in 2020.<p>
		<p>In many cases we have reverse geocoded observations available at high level of geographical resolution (for example, the geographical coordinates of a higher education institution) using NUTS2 boundary files available from Eurostat. When doing this, we have assigned observations to regions in the NUTS2 version that was in use at the time when the data were collected / when the events captured in the data took place.<p>

		<h2>Data processing</h2>

		<p>In general, we have avoided complex data processing beyond what was required to aggregate data at our preferred level of geographical resolution. There are however a couple of exceptions to this:<p>

		<ul>
			<li>
				<p>We have calculated indices of economic complexity for UK regions used the algorithm developed by <ExternalLink href={HausmanAndHidalgoUrl} text='Hausman and Hidalgo (2009)'/>.<p>
			</li>
			<li>
				<p>We have measured levels of employment in entertainment and cultural sectors using an industrial segmentation based on the methodology developed by <ExternalLink href={DelgadoEtAlUrl} text='Delgado et al (2015)'/>.<p>
			</li>
			<li>
				<p>We have identified UKRI-funded research projects in STEM disciplines using a machine learning analysis of project descriptions presented in <ExternalLink href={MateosGarciaUrl} text='Mateos-Garcia (2017)'/>.<p>
			</li>
		</ul>

		<p>We indicate those indicators based on experimental methodologies or data sources where relevant.<p>

		<div class='cta'>
			<LinkButton
				url='/download'
				text='Download all indicators'
				withDownloadIcon={true}
			/>
			<LinkButton url='/guide' text='Read the guide' />
			<LinkButton url='/indicators' text='Explore the indicators' />
		</div>
	</section>
</main>

<style>
	main {
		height: 100%;
		width: 100%;
		display: flex;
		justify-content: space-around;

		font-size: 1.05rem;
		font-weight: 200;
		background-color: var(--color-background);
	}

	section {
		max-width: 900px;
		padding: 2rem;
		overflow-y: auto;
		background-color: white;
		box-shadow: var(--box-shadow-y);
	}

	h1 {
		font-family: 'Open Sans Semibold', sans-serif;
	}
	h2 {
		margin-bottom: 1.5rem;
		margin-top: 1.5rem;
		font-family: 'Open Sans Regular', sans-serif;
	}

	p {
		margin-bottom: 1.5rem;
	}

	a {
		text-decoration: none;
		font-weight: bold;
	}

	p a {
		padding: 0.1rem;
		border-bottom: 1px solid var(--color-link);
		color: var(--color-link);
		text-decoration: none;
		font-weight: bold;
	}

	ul {
		list-style: initial;
		margin-left: 20px;
	}

	.cta {
		display: flex;
		justify-content: space-around;
		margin: 4rem 0 3rem 0;
		flex-direction: column;
		row-gap: 1em;
	}

	.large .cta {
		flex-direction: row;
		row-gap: 0;
	}
</style>
