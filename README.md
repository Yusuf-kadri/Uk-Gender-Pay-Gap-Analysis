# UK Gender Pay Gap Analysis (2025–26)

**Question:** How large is the gender pay gap across UK employers, and does it differ between sectors or between employers who report on time and those who report late?

All UK employers with 250+ staff must publish their gender pay gap each year. This project cleans that data, explores it visually, and tests whether the differences we see are statistically meaningful.

---

## Data

- **Source:** [UK Government Gender Pay Gap Service](https://gender-pay-gap.service.gov.uk/), 2025–26 reporting year
- **Size:** 11,193 employer returns
- **Key variable:** `DiffMeanHourlyPercent`, the percentage difference between men's and women's mean hourly pay

## Approach

1. **Cleaning** (`readr`, `dplyr`)
   - Identified public sector employers from blank company numbers
   - Ordered employer size as a factor
   - Checked the late-submission flag against the actual submission dates
2. **Exploration** (`ggplot2`)
   - Plotted the distribution of the pay gap before any testing
   - Spotted a data quality issue: some employers' male and female bonus figures sum to exactly 100%, which suggests the form question was misread
3. **Testing** (`t.test()`)
   - Is the average gap different from zero?
   - Public sector v business/charity
   - Late v on-time reporters

## Findings

| Comparison | Result |
|---|---|
| Average gap across all employers | **11.5%** in favour of men, t(11192) = 76.1 |
| Public sector v business/charity | 10.92% v 11.59%, t(2813) = 2.07, p = .0385 |
| Late v on-time reporters | 9.93% v 11.60%, t(705.96) = −1.36, p = .176 |

- The gap is clearly above zero.
- Business and charity employers show a gap about 0.7 percentage points larger than the public sector. The difference is statistically significant, but small.
- There is no evidence that late reporters have a different gap from on-time reporters.

![Distribution of the gender pay gap](figures/pay-gap-distribution.png)
*Figure 1. Mean hourly pay gap by employer. Four observations below −100% are omitted.*

![Pay gap by sector](figures/pay-gap-by-sector.png)
*Figure 2. Pay gap distribution by sector, with group means marked.*

## Repository structure

```
uk-gender-pay-gap-analysis/
├── README.md
├── analysis.Rmd        # full analysis
├── analysis.md         # knitted output (renders on GitHub)
├── data/               # or see the link above
└── figures/
```

## How to run

Install the packages, then knit `analysis.Rmd`:

```r
install.packages(c("tidyverse", "knitr"))
```

## Tools

R · tidyverse (readr, dplyr, ggplot2) · knitr
