# Using Astropy and Gaia DR3 to make an H-R diagram

Make an observed Hertzsprung-Russell diagram for Gaia DR3 stars within 100pc of the Sun with <1% parallax
precision and apparent G >18 magnitude. This selects ~200k stars.

Uses `astroquery` to retrieve the data from the Gaia DR3 database. With a fast (>500Mbps) ethernet connection
and normal Gaia server load, the query to retrieve ~200k stars takes 20 to 60 seconds.

## Gaia DR3 data query

Gaia DR3 query for nearby stars as follows:
 * stars within 100pc ($\varpi\ge$ 10 mas)
 * parallax uncertainty <1% ($\varpi/\sigma_\varpi\ge$ 100)
 * apparent magnitude $m_G$<18
 * BP and RP fluxes with SNR>10 ($F_x/\sigma_{F_x}\ge$10)
 * proper motions with SNR>10 ($|\mu_x/\sigma_{\mu_x}|\ge$10)
 * Renormalised Unit Weight Error (RUWE) < 1.4

This query returns about 200k stars and takes ~15-60 seconds depending on the server load and your
internet speed.  We time the query and report how many stars we retrieved.

The query returns 4 columns of data:
 * `color` = BP$-$RP color index
 * `mg` = absolute G magnitude (M$_G$) computed using the apparent mean G magnitude and parallax
 * `parallax` $\varpi$ in mas
 * `parallax_error` $\sigma_\varpi$ in mas

We do an additional cut, following Torres et al. 2022, that removes parallaxes within 3$\sigma$ of our
100pc cutoff: $\varpi - 3*\sigma_\varpi \ge 10$
